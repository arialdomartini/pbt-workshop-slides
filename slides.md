---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: img/background.jpg
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
lineNumbers: true
---

# PropertyPlastico

<span style="background-color: #FF0;
  padding:.5em;color:black;font-weight: bold;font-size:1em;">
  Un workshop introduttivo a Property-Based Testing
</span>

---


# Agenda

<div v-click style="zoom:.75;">

> **Teoria** (ma con codice)
>  * Example Based vs Property Based
>  * Esempi di codice (in C#)

<br/>
</div>
<div v-click style="zoom:.75;">

> **Pratica: Limiti di TDD**
>  * Il Prime Factor Kata di Robert Martin
>    * In TDD by the book
>    * In PBT

<br/>
</div>
<div v-click style="zoom:.75;">


> **Teoria**
>  * Theory, Fixture, auto-fixture, generatori, shrinker
>    * Generatori (a manella)
>    * Anatomia di un property test
>    * Catturare proprietà
>    * Enterprise Developer from Hell di Scott Wlaschin

<br/>
</div>
<div v-click style="zoom:.75;">

> **Pratica: Design Emergente**
>  * Il Print Diamond Kata

<br/>
</div>
<div v-click style="zoom:.75;">

> **Pratica: caso reale**
>  * Supermarket Kata di Ferdinando Santacroce

</div>

---
layout: section
---

# Takeaway

---

# Testi verdi → pronti per il deploy?

<div style="margin-left:auto; margin-right: auto; width:35%">
    <figure>
        <img src="./img/all-green-tests.png" >
    </figure>
</div>

---

# TDD is not about testing

<br/>
<div style="margin-left:auto; margin-right: auto; width:50%">
    <figure>
        <img src="./img/luca-pacioli.jpg" >
        <figcaption><center>Luca Pacioli (1455-1517)</center></figcaption>
    </figure>
</div>


---

# Test == requisiti


```csharp
[Fact]
void sum()
{
    Assert.Equal(5, Sum(2, 3));
}
```

<br/>

```csharp
[Fact]
void factors()
{
    Assert.Equal([],        FactorsOf(1));
    Assert.Equal([2],       FactorsOf(2));
    Assert.Equal([3],       FactorsOf(3));
    Assert.Equal([2, 2],    FactorsOf(4));
    Assert.Equal([5],       FactorsOf(5));
    Assert.Equal([2, 3],    FactorsOf(6));
    Assert.Equal([7],       FactorsOf(7));
    Assert.Equal([2, 2, 2], FactorsOf(8));
    Assert.Equal([3, 3],    FactorsOf(9));
}
```



---
layout: two-cols-header
---

# Takeaway

::left::

## Teoria

<v-clicks>

- `Theory > n * Fact`
- Non servono librerie

</v-clicks>

::right::

## Coding sessions

<v-clicks>

- **Prime Factors Kata**<br/> completezza, affidabilità, production readiness
- **Print Diamond Kata**<br/> design emergente, sviluppo incrementale
- **Supermarket Kata**<br/> cogliere l'essenza dei requisiti

</v-clicks>

---
layout: section
---

# TDD ≠ Requisiti come codice

---
transition: none
---

# Slide per PM e C-level

<div style="margin-left:auto; margin-right: auto; width:95%">
    <figure>
        <img src="./img/k/1.png" >
    </figure>
</div>

---
transition: none
---

# Slide per PM e C-level

<div style="margin-left:auto; margin-right: auto; width:95%">
    <figure>
        <img src="./img/k/2.png" >
    </figure>
</div>

---
transition: none
---

# Slide per PM e C-level

<div style="margin-left:auto; margin-right: auto; width:95%">
    <figure>
        <img src="./img/k/3.png" >
    </figure>
</div>

---
transition: none
---

# Slide per PM e C-level

<div style="margin-left:auto; margin-right: auto; width:95%">
    <figure>
        <img src="./img/k/4.png" >
    </figure>
</div>

---
transition: none
---

# Slide per PM e C-level

<div style="margin-left:auto; margin-right: auto; width:95%">
    <figure>
        <img src="./img/k/5.png" >
    </figure>
</div>

---
transition: none
---

# Slide per PM e C-level

<div style="margin-left:auto; margin-right: auto; width:95%">
    <figure>
        <img src="./img/k/6.png" >
    </figure>
</div>

---

# Slide per PM e C-level

<div style="margin-left:auto; margin-right: auto; width:95%">
    <figure>
        <img src="./img/k/7.png" >
    </figure>
</div>


<div style="position:absolute; top:400px; left:555px; width:100px;">
    <figure>
        <img src="./img/k/robot.gif" >
    </figure>
</div>

---

# Requisito #1

###  Regola generale
> Il catalogo mostra sempre un elenco di prodotti<br/>
> in ordine alfabetico  


<br/>
<div v-click>

### Esempio concreto

> Per esempio: se il catalogo contiene i prodotti:<br/>
> * Muffin
> * Caffè
> * Latte<br/><br/>
> devono essere mostrati come:<br/><br/>
> * Caffè
> * Latte
> * Muffin

</div>
---

# Requisito #2

###  Regola generale
> Gli account name sono unici e case insensitive

<br/>
<div v-click>

### Esempio concreto
> Per esempio, non si possono avere 2 `john.doe`<br/>
> Inoltre, `john.doe` e `JOHN.DOE` sono lo stesso account.

</div>

---

# Requisito 3

###  Regola generale
> Non applichiamo mai più di una promozione a un acquisto;<br>
>selezioniamo sempre lo sconto più conveniente per il cliente.

<br/>

<div v-click>

### Esempio concreto
> Supponiamo che un cliente acquisti 2 tazze di caffè, 1 latte e 1
muffin per 4 persone.<br/>
> 4 persone hanno diritto alla Promozione "Famiglia", sconto del 20%, 1
EUR.<br/>
> Latte e Muffin attivano la Promozione "Colazione", 0.8 EUR.<br/>
>In questo caso, applichiamo la Promozione "Famiglia", perché è la più conveniente

</div>

---
layout: section
---

# Esempi di traduzione da Example-Based a Property-Based

---


# Un Property Test di esempio: repository

<div v-click="1">

> Quando un prodotto viene salvato<br/>
> può essere ricaricato dal disco tramite il suo ID.

<br/>
</div>

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


<div v-click="1">

> I multipli di 15<br/>
> producono "fizzbuzz"

<br/>
</div>


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

```csharp
[Property]
Property multiples_of_15_return_fizzbuzz(int n)
{
   var multipleOf15 = n * 15;

   return fizzbuzz(multipleOf15) == "fizzbuzz";
}
```


```csharp {all|2|6|9}
[Property]
Property multiples_of_15_return_fizzbuzz()
{
    var multiplesOf15 = Arb.From( 
        Arb.Generate<int>()
           .Select(i => i * 15));

    return Prop.ForAll(multiplesOf15, n => 
        fizzbuzz(n) == "fizzbuzz");
}
```
````

---
transition: none
---

# Property Test di esempio: account unici e case insensitive

> Gli account name sono unici e case insensitive.<br/>
> Per esempio, non si possono avere 2 `john.doe`.<br/>
> Inoltre, `john.doe` e `JOHN.DOE` sono lo stesso account.<br/>

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
transition: none
---


# Property Test di esempio: account unici

> Gli account name sono unici e case insensitive.<br/>
> Per esempio, non si possono avere 2 `john.doe`.<br/>

<br/>

```csharp
[Property]
bool account_names_are_unique(List<Employee> employees)
{
    var accountNames = employees.Select(AccountNameGenerator.Generate);

    return accountNames.ContainNoDuplicates();
}

bool ContainNoDuplicates(IEnumerable<string> xs) =>
    xs.SequenceEqual(xs.Distinct());
```

---

# Property Test di esempio: account case insensitive

> Gli account name sono unici e case insensitive.<br/>
> Per esempio, non si possono avere 2 `john.doe`.<br/>

<br/>

```csharp
[Property]
bool account_names_are_case_insensitive_(Employee employee)
{
    var accountName = AccountNameGenerator.Generate(employee);

    var upper = accountName.ToUpper();
        
    return AuthenticationSystem.Login(upper);
}
```

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

---

# Lati negativi

* Difficile.
* Capire cosa sia una proprietà a volte non è banale.
* Una nicchia di una nicchia.

---
layout: section
---

# Cos'è una proprietà?

---

# Non è una questione di casualità

Fuzzy Generation != killer feature

> Per questioni legali  
> i prodotti alimentari non possono essere parte di spedizioni internazionali  
> a meno che non ci sia una promozione attiva.

<br/>

```csharp
if(product.Type == Food && order.Destination != LocalCountry)
    throw new CannotBeSentException();
```

C'è un bug?

---

# Verifica di una proprietà

<v-clicks>

* Logic, come in Prolog
* Theory Prover
* AI
* Concolic Testing
* Brute force
* niente

</v-clicks>

---
layout: section
---

# Coding Session<br/>Prime Factors Kata

---
layout: two-cols-header
---

# Prime Factors Kata - Osservazioni

Quale approccio cattura meglio il requisito?

::left::

<div style="margin-right:.5em;">
```csharp
[Fact]
void factors()
{
    Assert.Equal([],        FactorsOf(1));
    Assert.Equal([2],       FactorsOf(2));
    Assert.Equal([3],       FactorsOf(3));
    Assert.Equal([2, 2],    FactorsOf(4));
    Assert.Equal([5],       FactorsOf(5));
    Assert.Equal([2, 3],    FactorsOf(6));
    Assert.Equal([7],       FactorsOf(7));
    Assert.Equal([2, 2, 2], FactorsOf(8));
    Assert.Equal([3, 3],    FactorsOf(9));
}
```
</div>

::right::

<div style="margin-left:.5em;">
```csharp
[Property]
bool boolean_factorization_in_prime_numbers(PositiveInt n)
{
    var factors = FactorsOf(n.Item);

    return
        factors.All(IsPrime) && 
        factors.Multiplied() == n;
}
```
</div>

---

# Prime Factors Kata - Osservazioni

<v-clicks>

- Sviluppo incrementale del codice e del test.
- Quale il più economico? (casi 6, 7, 8)
- PBT ha guidato lo sviluppo? Ruolo dello shrinker
- Fake it until you make it
- Quando i test sono abbastanza test?
- Il design è stato emergente?
- Test verde == rilascio in produzione?

</v-clicks>

---
layout: two-cols-header
---

# Dal punto di vista della Production Readiness

::left::

<div style="margin-left:auto; margin-right: auto; width:75%">
    <figure>
        <img src="./img/incremental-reality.png" >
        <figcaption><center>La realtà</center></figcaption>
    </figure>
</div>

::right::

<div v-click style="margin-left:auto; margin-right: auto; width:75%">
    <figure>
        <img src="./img/incremental-example-based.png" >
        <figcaption><center>Il feedback che abbiamo avuto da TDD</center></figcaption>
    </figure>
</div>

---
transition: none
---

# Prime Factors Kata - codice allo step 3

<div style="zoom: 100%;">
```csharp
private static List<int> FactorsOf(int n) =>
        n > 1 ? [n] : [];
```
</div>

---
transition: none
---

# Prime Factors Kata - codice allo step 3

<div style="margin-left:auto; margin-right: auto; width:75%">
        <img src="./img/prime-factors-bugged-code-hidden.png" >
</div>

---
---

# Prime Factors Kata - codice allo step 3

<div style="margin-left:auto; margin-right: auto; width:75%">
        <img src="./img/prime-factors-bugged-code.png" >
</div>

---

# Collateral property


- `factorize(prime) -> [prime]`
- `factorize(prime^2) -> [prime, prime]`
- `factorize(prime^n) -> [prime, ..., prime]`
- `factorize(prime1 * prime2) -> [prime1, prime2]`
- `factorize(prime1 * .... * primeN) -> [prime1, ..., primeN]`
- `factorize(n < 2) -> IllegalArgumentException`
- `factorize(2 <= number <= Integer.MAX_VALUE) -> no exception  `
- `product of all returned numbers must be equal to input number`
- `all numbers in produced list must be primes`

---
layout: section
---

# Fixtures, Properties<br/>Generators, Shrinkers

---

# Fixture

````md magic-move {lines: true}
```csharp
[Fact]
void calcutates_the_sum_of_2_numbers()
{
    var sum = Add(2, 3);
    
    Assert.Equal(5, sum);
}
```

```csharp
[Theory]
[InlineData(2, 3, 5)]
[InlineData(2, 0, 2)]
[InlineData(0, 2, 2)]
[InlineData(2, -2, 0)]
[InlineData(9999, -2, 9997)]
void calcutates_the_sum_of_2_numbers(int a, int b, int expectedSum)
{
    var sum = Add(a, b);
    
    Assert.Equal(expectedSum, sum);
}
```
````

---


# Auto-Fixture con regole di dominio


```csharp
[Theory]
[AutoData]
void any_product_classified_as_food_is_discountable([Food] Product product)
{
    Assert.True(_catalog.CanBeDiscounted(product));
}
```

---

# Fixture: non possono usare tipi non primitivi

> Food products can be discounted

```csharp
[Theory]
[InlineData(
    new Product(
        name: "Apple",
        category: Categories.Fruits,
        price: 0.90,
        description: "Delicious Fuji apple"))
[InlineData(
    new Product(
        name: "'Nduja",
        category:
        Categories.Sausages,
        price: 9.50,
        description: "Spicy. Original from Calabria"))
        
void discountable_products(Product product)
{
    var discountIsApplyed = _catalog.CanBeDiscounted(product);
    
    Assert.True(discountIsApplyed);
}
```

---


# Proprietà: non solo una questione di auto-fixture

```csharp
[Theory]
[InlineData(   2,  3,    5)]
[InlineData(   2,  0,    2)]
[InlineData(   0,  2,    2)]
[InlineData(   2, -2,    0)]
[InlineData(9999, -2, 9997)]
void calcutates_the_sum_of_2_numbers(int a, int b, int expectedSum)
{
    var sum = Add(a, b);
    
    Assert.Equal(expectedSum, sum);
}
```

<br/>

```csharp
[Property]
void calcutates_the_sum_of_2_numbers(int a, int b)
{
    var sum = Add(a, b);
    
    Assert.Equal(???, sum);
}
```


---

# Scelte deboli

```csharp
[Property]
void calcutates_the_sum_of_2_numbers(int a, int b)
{
    var sum = Add(a, b);
    
    var expected = a + b;
    
    Assert.Equal(expected, sum);
}
```

<br/>

```csharp
int Add(int a, int b) =>
    a + b;
```

<br/>

<div v-click>
```csharp
[Fact]
void calcutates_the_sum_of_2_numbers()
{
    var sum = Add(2, 3);
    
    Assert.Equal(5, sum);
}
```
</div>


---
layout: section
---

# Non abbiamo mai capito le Theory

---


# Fixture: Theory?

> "Theories are tests which are only true for a particular set of
> data."

<arrow v-click="[2,3]" x1="400" y1="140" x2="345" y2="190" color="#953" width="2" arrowSize="1" style="z-index: 9999;"/>

<div v-click="1">
```csharp
[Theory]
[InLineData(2, 2, 4)]
[InLineData(5, 7, 12)]
void sum(int a, int b, int expectedValue)
{
    ....
    AssertEqual(expectedValue, result);
}
```
</div>

<br/>

<div v-click="3">

```csharp
  [Theory]
  [InlineData(5, 1, 3, 9)]
  [InlineData(7, 1, 5, 3)]
  public void AllNumbers_AreOdd_WithInlineData(int a, int b, int c, int d)
  {
      Assert.True(IsOddNumber(a));
      Assert.True(IsOddNumber(b));
      Assert.True(IsOddNumber(c));
      Assert.True(IsOddNumber(d));
  }
}
```

</div>

---
transition: none
---

# Fixture: Theory!

<br/><br/>

<div style="margin-left:auto; margin-right: auto; width:100%">
        <img src="./img/theory.png" >
</div>

<br/><br/><br/>

## References
* [Why Did we Build xUnit 1.0?](https://xunit.net/docs/why-did-we-build-xunit-1.0)
* [Why the word "Theory" as opposed to something like "MultiFact"? #2822](https://github.com/xunit/xunit/discussions/2822)


---

# Fixture: Theory!


<arrow x1="150" y1="230" x2="275" y2="260" color="#953" width="2" arrowSize="1" style="z-index: 9999;"/>

<div style="margin-left:auto; margin-right: auto; width:50%">
        <img src="./img/theory-abstract.png" >
</div>


## References
* [Theories in practice: Easy-to-write specifications that catch bugs](https://homes.cs.washington.edu/~mernst/pubs/testing-theories-tr002-abstract.html)

---
layout: section
---

# Idealmente

---

# Idealmente: attributi magici

```csharp
[Property]
void account_name_is_unique(
    [AllDifferent] Account[] existingAccounts, 
    [FormWithDuplicatedAccount] RegistrationForm form)
{
    var validationResult = _register(form);
    
    Assert.Equal(Error("Account already exists"), validationResult);
}
```


---

# Idealmente: attributi magici

```csharp
[Property]
void no_discounts_is_applied_to_carts_without_food(
    [CartContainingNoFoodProducts] List<Product> products)
{
    var plainSumOfPrices = products.Sum(p => p.Price);
    _cart.Add(products)
    
    var total = _cart.Checkout();
    
    Assert.Equal(plainSumOfPrices, total)
}
```

---

# Idealmente: Controesempi con Shrinking


````md magic-move {lines: true}
```csharp
I found a counterexample!
Here it is:


  new Product(
    Name: "\0.",
    Category: Categories.SoftDrinks,
    Price: 192722,
    Description: "11111111A\0")}
```

```csharp
I get the general rule. But, hey! I found a counterexample!
Here it is:

  new Product(
    Name: _,
    Category: Categories.SoftDrinks,
    Price: _,
    Description: _)}


Don't even care about `name`, `price` and other fields: the element 
causing the problem is 

   category = Categories.SoftDrinks


Apparently, the production code is not considering soft drinks as a food.<br/>
Either this is a bug, or your specification is incomplete.
```
````


---

# Funzioni ad-hoc

```csharp
[Fact]
void account_name_is_unique()
{
    Account[] existingAccounts = GenerateAllDifferent();
    RegistrationForm form = GenerateWithADuplicateFrom(existingAccounts);

    _application.Accounts = accounts;

    var validationResult = _register(form);
    
    Assert.Equal(Error("Account already exists"), validationResult);
}
```

---

# Funzioni ad-hoc

```csharp
record Input(Account[] ExistingAccounts, RegistrationForm form)

[Fact]
void account_name_is_unique()
{
    Input[] inputs = Generate(10_000);

    inputs.ForEach(input =>
        _application.Accounts = input.accounts;

        var validationResult = _register(input.Accounts, input.Form);
    
        Assert.Equal(Error("duplicated"), validationResult);
    )
}
```

---

# Funzioni ad-hoc: non compongono


```csharp
    Account[] existingAccountsIncludingDisabledOnes = 
        GenerateAllDifferent()
            .ComposedWith(HavingAtLeast3DisabledAccounts());
```

---

# Nella realtà

- Type-Driven Design
- Properties (Essential Properties and Collateral Properties)
- Generators

---

# Nella realtà: Type-Driven Design

````md magic-move {lines: true}
```csharp
[Property]
void no_discounts_is_applied_to_carts_without_food(
    [CartContainingElectronicProducts] List<Product> products)
{
    var plainSumOfPrices = products.Sum(p => p.Price);
    _cart.Add(products)
    
    var total = _cart.Checkout();
    
    Assert.Equal(plainSumOfPrices, total)
}
```

```csharp
[Property]
void no_discounts_is_applied_to_carts_without_food(
    List<ElectronicProduct> products)
{
    var plainSumOfPrices = products.Sum(p => p.Price);
    _cart.Add(products)
    
    var total = _cart.Checkout();
    
    Assert.Equal(plainSumOfPrices, total)
}
```
````

---


# Nella realtà: Generators

```csharp
    Account[] existingAccountsIncludingDisabledOnes = 
        GenerateAllDifferent()
            .ComposedWith(HavingAtLeast3DisabledAccounts());
```

<br/>

<div v-click>

```csharp
    Gen<Account[]> existingAccountsIncludingDisabledOnes = 
        from accounts in Gen.ListOf(GenAccount)
        let distinct = accounts.Distinct()
        where distinct.Count(a => a.IsDisabled) >= 3
        select distinct;
```

</div>

---

# Nella realtà: Generators

```fsharp
record User(int Id, string FirstName, string LastName);

Gen<User> users =
    from fistName in Gen.Elements("Don", "Henrik", null)
    from secondName in Gen.Elements("Syme", "Feldt")
    from id in Gen.Choose(0, 1000)
    select new User(id, firstName, secondName);
```

---




# Generatori

```csharp
Generator :: Random -> Size -> data
```

---

# Caso reale di uso di generatori

````md magic-move {lines: true}
```csharp {all|7,9|all}
record Product(Guid Id, string Name, decimal Price, Category category);

Gen<Product> products =
    from id in Arb.Generate<Guid>()
    from name in Arb.Generate<string>()
    from price in Arb.Generate<decimal>()
    from category in Arb.Generate<Category>()
	
    select new Product(Id: id, Name: name, Price: price, Category: category);
```

```csharp
record Product(Guid Id, string Name, decimal Price, Category category);

[Property]
Property some_property_about_products()
{
    Gen<Product> products =
        from id in Arb.Generate<Guid>()
        from name in Arb.Generate<string>()
        from price in Arb.Generate<decimal>()
        from category in Arb.Generate<Category>()
    	
        select new Product(Id: id, Name: name, Price: price, Category: category);
        
    return ForAll(products.ToArbitrary(), product => 
        somePropertyOf(product));
}
```


```csharp
record Product(Guid Id, string Name, decimal Price, Category category);

[Property]
bool some_property_about_products(Product product)
{
    return somePropertyOf(product));
}
```


```csharp
record Product(Guid Id, string Name, decimal Price, Category category);

[Property]
bool some_property_about_products(Product product) =>
    somePropertyOf(product));
```

````


---
layout: section
---

# Scrivere property test

---


# Anatomia di un property test

```csharp {all|2|6|8|8,4|all}
[Property]
Property square_of_numbers_are_non_negative()
{
    Arbitrary<int> numbers = Arb.From<int>();

    int square(int n) => n * n;

    return ForAll(numbers, n => square(n) >= 0;);
}
```
---
transition: none
---

# Anatomia di un property test

```csharp
[Property]
Property square_of_numbers_are_non_negative()
{
    Arbitrary<int> numbers = Arb.From<int>();

    int square(int n) => n * n;

    bool squareIsNotNegative(int n) => square(n) >= 0;

    return ForAll(numbers, squareIsNotNegative);
}
```

---
transition: none
---

# Anatomia di un property test

```csharp
[Property]
Property square_of_numbers_are_non_negative() =>
    ForAll(Arb.From<int>(), n => square(n) >= 0);
```

---
transition: none
---

# Anatomia di un property test

```csharp
[Property]
bool square_of_numbers_are_non_negative(int n) =>
    square(n) >= 0;
```


---
transition: slide-left
---


# Property: la somma

```csharp
[Property]
void calcutates_the_sum_of_2_numbers(int a, int b)
{
    var sum = Add(a, b);
    ???
}
```

<br/>

```csharp
int Add(int a, int b) =>
    a + b;
```

---
layout: section
---

# Individuare le proprietà

---

# Essential Property e Collateral Property

### Essential

```csharp
[Property]
Property all_the_multiples_of_15_return_fizzbuzz()
{
    var multiplesOf15 = Arb.From( 
        Arb.Generate<int>()
            .Select(i => i * 15));

    return Prop.ForAll(multiplesOf15, n => 
        fizzbuzz(n) == "fizzbuzz");
}
```

<br/>

### Collateral

```csharp
[Property]
bool rev_rev(List<int> xs) =>
    Reverse(Reverse(xs)).SequenceEqual(xs);
```


---

# Essential Property

### È un approccio mentale, non una libreria


| Strategia                                              | Effetto                                             |
|--------------------------------------------------------|-----------------------------------------------------|
| `[Theory]` (senza `expectedResult`) invece di `[Fact]` | Non si può fare affidamenteo sul valore atteso      |
| Conceiling Methods                                     | Non si mostrano i valori di ingresso                |
| Random Values Factories                                | Non si può fare affidamenteo sui valori di ingresso |


---

# Theory senza expectedResult


<div style="zoom:75%">

````md magic-move {lines: true}
```csharp
[Theory]
[InlineData("1.0", "1.5", ".8", "1.0")]
[InlineData("1.0", "1.5", "1.0", "1.0")]
[InlineData("1.0", "1.5", "1.2.5", "1.2.5")]
[InlineData("1.0", "1.5", "1.5", "1.5")]
[InlineData("1.0", "1.5", "1.9", "1.5")]
[InlineData("1.0", "1.1", "1.0.5", "1.0.5")]
[InlineData("1.0", "1.1", "", "1.0")]
public void ProtocolResolvesCorrectly(string minProtocol, string maxProtocol, string clientProtocol, string expectedProtocol)
{
    var request = new Mock<IRequest>();
    var queryStrings = new NameValueCollection();
    var minProtocolVersion = new Version(minProtocol);
    var maxProtocolVersion = new Version(maxProtocol);
    var protocolResolver = new ProtocolResolver(minProtocolVersion, maxProtocolVersion);

    queryStrings.Add("clientProtocol", clientProtocol);

    request.Setup(r => r.QueryString).Returns(new NameValueCollectionWrapper(queryStrings));

    var version = protocolResolver.Resolve(request.Object);

    Assert.Equal(version, new Version(expectedProtocol));
}
```


```csharp
[Theory]
[InlineData("1.0", "1.5", ".8")]
[InlineData("1.0", "1.1", "")]
public void default_to_minimum_protocol_if_client_is_out_of_date_or_unspecified(string minProtocol, string maxProtocol, string clientProtocol)
{
    var request = new Mock<IRequest>();
    var queryStrings = new NameValueCollection();
    var minProtocolVersion = new Version(minProtocol);
    var maxProtocolVersion = new Version(maxProtocol);
    var protocolResolver = new ProtocolResolver(minProtocolVersion, maxProtocolVersion);

    queryStrings.Add("clientProtocol", clientProtocol);

    request.Setup(r => r.QueryString).Returns(new NameValueCollectionWrapper(queryStrings));

    var version = protocolResolver.Resolve(request.Object);

    Assert.Equal(version, new Version(minProtocol));
}
```

```csharp

[Theory]
[InlineData("1.0", "1.5", "1.0")]
[InlineData("1.0", "1.5", "1.2.5")]
[InlineData("1.0", "1.5", "1.5")]
[InlineData("1.0", "1.1", "1.0.5")]
public void prefer_client_protocol_if_compatible(string minProtocol, string maxProtocol, string clientProtocol)
{
    var request = new Mock<IRequest>();
    var queryStrings = new NameValueCollection();
    var minProtocolVersion = new Version(minProtocol);
    var maxProtocolVersion = new Version(maxProtocol);
    var protocolResolver = new ProtocolResolver(minProtocolVersion, maxProtocolVersion);

    queryStrings.Add("clientProtocol", clientProtocol);

    request.Setup(r => r.QueryString).Returns(new NameValueCollectionWrapper(queryStrings));

    var version = protocolResolver.Resolve(request.Object);

    Assert.Equal(version, new Version(clientProtocol));
}
```


```csharp
[Theory]
[InlineData("1.0", "1.5", "1.9", "1.5")]
public void never_use_a_protocol_beyond_maximum(string minProtocol, string maxProtocol, string clientProtocol)
{
    var request = new Mock<IRequest>();
    var queryStrings = new NameValueCollection();
    var minProtocolVersion = new Version(minProtocol);
    var maxProtocolVersion = new Version(maxProtocol);
    var protocolResolver = new ProtocolResolver(minProtocolVersion, maxProtocolVersion);

    queryStrings.Add("clientProtocol", clientProtocol);

    request.Setup(r => r.QueryString).Returns(new NameValueCollectionWrapper(queryStrings));

    var version = protocolResolver.Resolve(request.Object);

    Assert.Equal(version, new Version(maxProtocol));
}
```
````

</div>


<arrow v-click="[1,2]" x1="400" y1="420" x2="325" y2="355" color="#953" width="2" arrowSize="1" style="z-index: 9999;"/>
<arrow v-click="[2,3]" x1="400" y1="440" x2="345" y2="375" color="#953" width="2" arrowSize="1" style="z-index: 9999;"/>
<arrow v-click="[3,4]" x1="400" y1="400" x2="325" y2="345" color="#953" width="2" arrowSize="1" style="z-index: 9999;"/>


<div v-click="4">
https://github.com/emadb/SignalR/blob/fd165078396d00c8ac3f5845445794d2605a8fdd/tests/Microsoft.AspNet.SignalR.Tests/Server/ProtocolResolverFacts.cs#L13
</div>

---

# Conceiling Methods

````md magic-move {lines: true}
```csharp
[Fact]
public void GetTotal_SameItemTwice_ShouldReturnTheSum()
{
    _priceListService.Setup(p => p
        .GetCurrentPriceFor(99))
        .Returns(100m);
            
    _cart.AddItem(99);
    _cart.AddItem(99);

    Assert.Equal(200m, _cart.Total);
}
```

```csharp
[Fact]
public void GetTotal_SameItemTwice_ShouldReturnTheSum()
{
    var someProduct = SomeProduct();
    _priceListService.Setup(p => p
        .GetCurrentPriceFor(someProducts.Id))
        .Returns(someProducts.Price);
            
    _cart.AddItem(someProduct.Id);
    _cart.AddItem(someProduct.Id);

    Assert.Equal(2 * someProduct.Price, _cart.Total);
}
```
````

<div v-click="2">
https://github.com/emadb/TddSerie/tree/master/src/CodicePlastico.TddSerie.Core.Tests
</div>
---

# Random Values Factories

````md magic-move {lines: true}
```csharp
[Fact]
public void GetTotal_SameItemTwice_ShouldReturnTheSum()
{
    var someProduct = SomeProduct();
    _priceListService.Setup(p => p
        .GetCurrentPriceFor(someProducts.Id))
        .Returns(someProducts.Price);
            
    _cart.AddItem(someProduct.Id);
    _cart.AddItem(someProduct.Id);

    Assert.Equal(2 * someProduct.Price, _cart.Total);
}
```

```csharp
[Fact]
public void GetTotal_SameItemNTimes_ShouldReturnTheSum()
{
    var (someProduct, quantity) = SomeProduct();
    _priceListService.Setup(p => p
        .GetCurrentPriceFor(someProducts.Id))
        .Returns(someProducts.Price);
            
    Enumerable.Range(1, quantity).ForEach(_ =>            
        _cart.AddItem(someProduct.Id););

    Assert.Equal(quantity * someProduct.Price, _cart.Total);
}
```

```csharp
[Property]
public bool GetTotal_SameItemNTimes_ShouldReturnTheSum(Product product, int quantity)
{
    _priceListService.Setup(p => p
        .GetCurrentPriceFor(someProducts.Id))
        .Returns(someProducts.Price);
            
    Enumerable.Range(1, quantity).ForEach(_ =>            
        _cart.AddItem(someProduct.Id););

    return _cart.Total == quantity * someProduct.Price;
}
```
````
---

# property: strategie

- Essential Properties
- Collateral Properties
  - Different paths, same destination
  - There and back again
  - Some things never change
  - The more things change, the more they stay the same
  - Solve a smaller problem first
  - Hard to prove, easy to verify
  - The test oracle

## References

- [Choosing properties for property-based testing](https://fsharpforfunandprofit.com/posts/property-based-testing-2/#different-paths)


---
transition: none
---

# Property: strategie - Different paths, same destination

<br/>

<div style="margin-left:auto; margin-right: auto; width:50%">
        <img src="./img/property_commutative.png" >
</div>

<br/><br/>

<div style="text-align: center; font-size: 2em;" v-click>
    Proprietà commutativa<br/>
    (Category Theory: commutative diagram)
</div>

---
transition: none
---

# Property: strategie - Different paths, same destination

<br/>

<div style="margin-left:auto; margin-right: auto; width:50%">
        <img src="./img/property_commutative.png" >
</div>

<br/><br/>

```csharp
[Property]
bool product(int n, int a, int b) =>
    n.Times(a).Times(b) == n.Times(b).Times(a);
```



---
transition: none
---

# Property: strategie - There and back again

<br/>

<div style="margin-left:auto; margin-right: auto; width:50%">
        <img src="./img/property_inverse.png" >
</div>


<br/><br/>

<div style="text-align: center; font-size: 2em;" v-click>
    Inverso / Isomorfismo
</div>

---


# Property: strategie - There and back again

<br/>

<div style="margin-left:auto; margin-right: auto; width:50%">
        <img src="./img/property_inverse.png" >
</div>


<br/>

````md magic-move {lines: true}
```csharp
[Property]
bool serialization(Product product) {
    var json = Json.Serialize(product);
    var obj = Json.Deserialize<Product>(json);
    
    return obj == product;
}
```

```csharp
[Property]
bool serialization(Product product) =>
    product.Serialize().Deserialize() == product;
```

```csharp
[Property]
bool all_products_can_be_persisted(Product product)
{
    _repository.Save(product);

    var found = _repository.LoadById(product.Id);

    return found == product;
}
```

```csharp
[Property]
bool all_products_can_be_persisted(Product product) =>
    _repository.LoadById(_repository.Save(product)) == product;
```
````

---
transition: none
---

# Property: strategie - Some things never change

<br/>


<div style="margin-left:auto; margin-right: auto; width:50%">
    <img src="./img/property_invariant.png" >
</div>


<br/>

<div style="text-align: center; font-size: 2em;" v-click>
    Invarianza
</div>

---


# Property: strategie - Some things never change

<br/>


<div style="margin-left:auto; margin-right: auto; width:50%">
    <img src="./img/property_invariant.png" >
</div>


<br/>

````md magic-move {lines: true}
```csharp
[Property]
bool sort_preserves_elements(List<int> xs) =>
    xs.Sort().Length == xs.Length;
```

```csharp
[Property]
bool preserves_amount_of_money(List<Product> products, Budget budget) {
    var cart = new Cart();
    
    var before = cart.Total + budget;
    
    products.ForEach(product => cart.Add(product));
    cart.Checkout(budget);
    
    var after = cart.Total + budget;
    
    return after == before;
}

```
````

---
transition: none
---

# Property: strategie - The more things change, the more they stay the same

<br/>


<div style="margin-left:auto; margin-right: auto; width:50%">
    <img src="./img/property_idempotence.png" >
</div>

<br/>

<div style="text-align: center; font-size: 2em;" v-click>
    Idempotenza
</div>


---

# Property: strategie - The more things change, the more they stay the same

<br/>


<div style="margin-left:auto; margin-right: auto; width:50%">
    <img src="./img/property_idempotence.png" >
</div>


<br/>

```csharp
[Property]
bool report_generation(List<Transaction> transactions)
{
    GenerateReports(transactions);
    var filesBefore = ReadReports();
    
    GenerateReports(transactions);
    var filesAfterSecondRun = ReadReports();

    return files == filesAfterSecondRun;
    
}
```

---
transition: none
---

# Property: strategie - Solve a smaller problem first

<br/>


<div style="margin-left:auto; margin-right: auto; width:50%">
    <img src="./img/property_induction.png" >
</div>


<br/>

<div style="text-align: center; font-size: 2em;" v-click>
    Induzione
</div>


---

# Property: strategie - Solve a smaller problem first

<br/>


<div style="margin-left:auto; margin-right: auto; width:50%">
    <img src="./img/property_induction.png" >
</div>


<br/>

```csharp
[Property]
bool n_apples_cost_n_times_50(PositiveInt n)
{
    int BuyTimes(int n) {
        var cart = new CheckoutSystem();
        Enumerable.Range(1, n).ForEach(_ => cart.Scan("apple"));
        var total = cart.Checkout();
        return total;
    }
    
    return BuyTimes(n + 1) == BuyTims(n) + 50;
}
```


---

# Property: strategie - Hard to prove, easy to verify



<div style="margin-left:auto; margin-right: auto; width:40%">
    <img src="./img/property_easy_verification.png" >
</div>


<div v-click>
```csharp
[Property]
Property works_with_tls()
{
    var certificates =
        from certificate in GenerateCertificate("my-domain")
        select certificate;
    
    return ForAll(certificates.ToArbitrary()), certificate => {
        InstallCertificate(certificate, "my-domain");
    
        var httpResponse = Get("https://my-domain");
    
        return httpResponse.StatusCode == OK;
    }
}
```

</div>
---

# Property: strategie - The test oracle

<div style="margin-left:auto; margin-right: auto; width:30%">
    <img src="./img/property_test_oracle.png" >
</div>


<div v-click>
```csharp
[Property]
bool login_logout(List<Operation> operations)
{
    foreach(var operation in operations)
    {
        _system.Do(operation);
        match operation with {
            Login  -> _model.LogIn();
            Logout -> _model.LogOut();
            Reset  -> _model.LogOut();
        }
    }

    return _system.IsAuthenticated == _model.IsAuthenticated;
}
```
</div>


---
layout: section
---

# Coding Session<br/>Design Emergente

## Con Print Diamond Kata

---

# Sviluppo incrementale

<br/>
<br/>

<div style="margin-left:auto; margin-right: auto; width:50%">
    <img src="./img/agile-car.png" >
</div>


---
layout: two-cols-header
---

# Considerazioni

::left::

<div style="margin-left:auto; margin-right: auto; width:75%">
    <figure>
        <img src="./img/tdd.png" >
        <figcaption><center>Property-Based Development - (Example)TDD</center></figcaption>
    </figure>
</div>


::right::

<div style="margin-left:auto; margin-right: auto; width:75%">
    <figure>
        <img src="./img/pbd.png" >
        <figcaption><center>Property-Based Development</center></figcaption>
    </figure>
</div>



---

# Property: la somma

```csharp
[Property]
void calcutates_the_sum_of_2_numbers(int a, int b)
{
    var sum = Add(a, b);
    
    return ???
}
```

<br/>

```csharp
int Add(int a, int b) =>
    a + b;
```


<div v-click>
<br/><br/>

- [Scott Wlaschin - The Enterprise Developer From Hell](https://fsharpforfunandprofit.com/posts/property-based-testing/)
- [Scott Wlaschin - An Introduction to Property-Based Testing](https://fsharpforfunandprofit.com/pbt/)
- [Scott Wlaschin - The lazy programmer's guide to writing thousands of tests](https://www.slideshare.net/slideshow/the-lazy-programmers-guide-to-writing-thousands-of-tests/232565051)
</div>

---
layout: section
---

# Coding session<br/>Supermarket Kata
## di Ferdinando Santacroce
