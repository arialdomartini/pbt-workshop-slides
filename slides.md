---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: PBT Workshop
info: |
  Un workshop introduttivo a Property-Based Testing
  
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# take snapshot for each slide in the overview
overviewSnapshots: true

---

# PBT Workshop

Un workshop introduttivo a Property-Based Testing

---

# Slide di KP

---

# Requisito #1

###  Regola generale
> Il catalogo mostra sempre un elenco di prodotti<br/>
> in ordine alfabetico  


<br/>

### Esempio concreto

> Per esempio: se il catalogo contiene i prodotti:<br/>
> * Muffin
> * Caffè
> * Latte<br/><br/>
> devono essere mostrati come:<br/><br/>
> * Caffè
> * Latte
> * Muffin

---

# Requisito #2

###  Regola generale
> Gli account name sono unici e case insensitive

<br/>

### Esempio concreto
> Per esempio, non si possono avere 2 `john.doe`.<br/>
> Inoltre, `john.doe` e `John.Doe` sono lo stesso account.

---

# Requisito 3

###  Regola generale
> Non applichiamo mai più di una promozione a un acquisto;<br>
>selezioniamo sempre lo sconto più conveniente per il cliente.

<br/>

### Esempio concreto
> Supponiamo che un cliente acquisti 2 tazze di caffè, 1 latte e 1
muffin per 4 persone.<br/>
> 4 persone hanno diritto alla Promozione 1, sconto del 20%, 1
EUR.<br/>
> Latte e Muffin attivano la Promozione 2, 0,8 EUR.<br/>
>In questo caso, applichiamo la Promozione 1, perché è la più conveniente


---

# Un Property Test di esempio: repository


````md magic-move {lines: true}
```csharp
record Product(Guid Id, string Name, Category Category, decimal Price);

[Fact]
void products_can_be_persisted()
{
    var product = new Product(
        Id: Guid.NewGuid(),
        Name: "The Little Schemer", 
        Category: Books, 
        Price: 16.50M);
    
    _repository.Save(product);

    var found = _repository.LoadById(product.Id);

    Assert.Equal(found, product);
}
```

```csharp
record Product(Guid Id, string Name, Category Category, decimal Price);

[Property]
bool all_products_can_be_persisted(Product product)
{
    _repository.Save(product);

    var found = _repository.LoadById(product.Id);

    return found == product;
}
```
````

---

# Un Property Test di esempio: Fizz Buzz


````md magic-move {lines: true}
```csharp
[Theory]
[InlineData(15)]
[InlineData(30)]
[InlineData(45)]
[InlineData(60)]
void multiples_of_15_return_fizzbuzz(int multipleOf15)
{
    Assert.Equal("fizzbuzz", fizzbuzz(multipleOf15));
}
```

```csharp {all|2|6,8}
[Property]
Property all_the_multiples_of_15_return_fizzbuzz()
{
    var multiplesOf15 = Arb.From( 
        Arb.Generate<int>()
            .Select(i => i * 15));

    return Prop.ForAll(multiplesOf15, n => fizzbuzz(n) == "fizzbuzz");
}
```
````



<span v-click="3">Multipli di 15 (Divisibili per 15) -> "FizzBuzz"</span>


---
transition: none
---

# Property Test di esempio:


> Gli account name sono unici e case insensitive.<br/>
> Per esempio, non si possono avere 2 `john.doe`.<br/>
> Inoltre, `john.doe` e `John.Doe` sono lo stesso account.<br/>

<br/>

```csharp
internal record Employee(string FirstName, string SecondName);

internal static class AccountNameGenerator
{
    private static string Generate(Employee employee) => ...
}

internal static class AuthenticationSystem
{
    private static bool Login(string accountName) => ...
}
```

---

# Property Test di esempio: account unici e case insensitive

> Gli account name sono unici e case insensitive.<br/>
> Per esempio, non si possono avere 2 `john.doe`.<br/>
> Inoltre, `john.doe` e `John.Doe` sono lo stesso account.<br/>

<br/>

```csharp
[Property]
bool account_names_are_unique(List<Employee> employees)
{
    var accountNames = employees.Select(AccountNameGenerator.Generate);

    return accountNames.ContainNoDuplicates();
}

[Property]
bool account_names_are_case_insensitive_(Employee employee)
{
    var accountName = AccountNameGenerator.Generate(employee);

    var upper = accountName.ToUpper();
        
    return AuthenticationSystem.Login(upper);
}
```

---
transition: slide-left
---

# Property Test di esempio: promozioni


> Non applichiamo mai più di una promozione a un acquisto;<br>
> selezioniamo sempre lo sconto più conveniente per il cliente

<br/>

```csharp {all|4,5|7|8|10|12-13|8,10,16-18}
[Property]
bool
we_never_apply_more_than_1_discount_and_we_always_select_the_most_convenient_discount(
    List<Product> products,
    List<Promotion> promotions)
{
    var cart = new Cart(promotions);
    var total = cart.Checkout(products);

    var otherTotals = promotions.Select(promotion =>
    {
        var singlePromotionCart = new Cart([promotion]);
        return singlePromotionCart.Checkout(products);
    }).ToList();

    return
        otherTotals.All(otherTotal => otherTotal >= total) &&
        otherTotals.Any(otherTotal => otherTotal == total);
}

```

---

# Esempio con generatore

```csharp {all|1-4|6-7|9-20|17|18|19|all}
private static readonly Gen<Product> SomeProducts =
    from s in Arb.Generate<NonEmptyString>()
    from p in Arb.Generate<Product>()
    select p with { Name = s.Get };

internal static readonly Gen<List<Product>> Assortments = from assortment in Gen.ListOf(SomeProducts)
    select assortment.DistinctBy(p => p.Name).ToList();

[Property]
Property the_catalog_always_lists_products_in_alphabetical_order() =>
    Prop.ForAll(Assortments.ToArbitrary(),
        assortmentOfProducts =>
        {
            var catalog = new Catalog(assortmentOfProducts);
             var listOfProducts = catalog.Products;
             return
                listOfProducts.EachProductIsLexicographicallyLessThanTheNext() &&
                listOfProducts.ContainsSameElementsOf(assortmentOfProducts) &&
                SortingAgainIsIdempotent(listOfProducts);
        });
```
