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

