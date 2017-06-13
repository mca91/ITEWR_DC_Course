---
title       : Mock Exam II
description : Dieses Testat besteht aus einem Kapitel mit insgesamt 8 Aufgaben. Die Aufgaben können unabhängig voneinander gelöst werden.

--- type:NormalExercise lang:r xp:100 skills:1 key:c4b2c27865
## Testatpunkte

Erinnern Sie sich an das letzte Testat: Es waren 1500XP zu erreichen. Angenommen Sie arbeiten als Hiwi am Lehrstuhl für Ökonometrie und Ihnen liegen Beobachtungen zur erreichten XP (`XP`) sowie investierter Zeit (`Z`) vor. In ihrer Schusseligkeit haben Sie einen zufälligen Teil der Daten unwiederbringlich gelöscht und wollen nun Regressionsanalyse & Inferenzstatistik anhand einer Stichprobe betreiben. Professor Dr. Prank pocht auf signifikante Ergebnisse, egal wie!
  <br>
  Der beobachtete Zusammenhang wird im Plot-Panel dargestellt.

Sie interessieren sich für das folgende Model:
  
  $$ XP\_i = \beta\_0 + \beta\_1 \times Z\_i +  \epsilon\_i  $$
  
  *Die Vektoren `XP` und `Z` sind in Ihrer Arbeitsumgebung verfügbar.*
  
 ***=hint

Lineare Modelle können Sie mit `lm` schätzen. Nutzten Sie `round` zum Runden. Die geschätzten Koeffizienten erhalten Sie z.B. mit `coefficients`.

***=instructions

Berechnen Sie die OLS-Schätzer für $\beta\_0$ und $\beta\_1$. Runden Sie die Werte auf *vier* Nachkommastellen. Speichern Sie die Ergebnisse in `beta0` und `beta1`.

*** =pre_exercise_code
```{r}
set.seed(2)
n <- 105
Z <- runif(n,0,24)
XP <- rep(NA,n)
for(i in 1:n) {
  XP[i] <- 100 + 60 * Z[i] + rnorm(1, sd=20*Z[i])
}
plot(Z,XP, pch=20, col="Steelblue", cex=1, xlim = c(0,24), ylim = c(0,1500), xlab="Zeitaufwand", ylab="XP")
```

***=sample_code
```{r}
# Berechnen Sie den Schätzer, speichern Sie die Ergebnisse in beta0 und beta1

```

***=solution
```{r}
beta0 <- round(lm(XP ~ Z)$coefficients[1],4)
beta1 <- round(lm(XP ~ Z)$coefficients[2],4)
```

*** =sct
```{r}
test_object("beta0", incorrect_msg = "Sie haben das Objekt falsch definiert.")
test_object("beta1", incorrect_msg = "Sie haben das Objekt falsch definiert.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:5826368309
## Übung macht den Meister? 

Sie befassen sich weiterhin mit dem Modell

$$ XP\_i = \beta\_0 + \beta\_1 \times Z\_i +  \epsilon\_i. $$
  
  Beim Betrachten des Plots kommt Ihnen etwas merkwürdig vor: Es scheint so, als ob die im Mittel erzielte XP zwar mit der investierten Zeit steigt, allerdings scheinen Studenten ohne Vorbereitungszeit mehr als 100XP zu erzielen.

Nun interessiert es Sie, ob die erwartete Punktzahl für Studenten, die gar keine Zeit investiert haben, signifikant von $0$ verschieden ist. Daher möchten Sie einen $t$-Test durchführen.

Hinweis: Es ist

$$ t \sim \tau_{n-k} $$
  
  wobei $\tau_{n-k}$ die $t$-Verteilung mit $n-k$ Freiheitsgraden ist.

*Die Vektoren `XP` und `Z` sowie ein entsprechendes Regressionsmodell `mod` sind in Ihrer Arbeitsumgebung verfügbar.*
  
  *** =pre_exercise_code
```{r}
set.seed(2)
n <- 105
Z <- runif(n,0,24)
XP <- rep(NA,n)
for(i in 1:n) {
  XP[i] <- 100 + 60 * Z[i] + rnorm(1, sd=20*Z[i])
}
mod <- lm(XP ~ Z)
```

***=instructions

- Berechnen Sie zunächst die passende $t$-Statistik zum Test $H\_0: \beta\_0=0 \ vs \ H\_1: \beta\_0\neq 0$. Benutzen sie *bei Homoskedastie gültige Standardfehler*. Runden Sie den Wert auf *vier* Nachkommastellen und speichern Sie das Ergebnis in `tstat`
- Überprüfen Sie mithilfe der Quantilsfunktion der $t$-Verteilung (`qt`) sowie logischer Operatoren, ob `tstat` im Ablehnbereicht eines Tests zum $5\%$-Niveau liegt. Vervollständigen Sie den Code. 

***=hint

Die Funktion `summary` liefert Ihnen statistische Informationen über ein Modellobjekt. Der Eintrag `coefficients` enthält eine Matrix mit geschätzten Koeffizienten sowie deren Standardfehler.<br>
  Nützliche logische Operatoren sind `<` oder `>`. Die Länge eines Vektors bestimmen Sie mit `length`. $k$ ist die Anzahl der Regressoren im Modell. Bedenken Sie: Es handelt sich um einen beidseitigen Test, d.h. sie suchen einen kritischen Wert $c\_{1-\frac{\alpha}{2}}$.

***=sample_code
```{r}
# Berechnen Sie die t-Statistik


# Überprüfen Sie, ob die t-Statistik Element des Ablehnbereichs ist
abs(tstat) >= ???

```

***=solution
```{r}
# Berechnen Sie die t-Statistik
tstat <- round(coefficients(summary(lm(XP ~ Z)))[1,3],4)

# Überprüfen Sie, ob die t-Statistik Element des Ablehnbereichs ist
abs(tstat) >= qt(0.975, df = 103)
```



*** =sct
```{r}
test_predefined_objects("XP", incorrect_msg = "Sie haben ein vordefiniertes Objekt manipuliert. Aktualisieren Sie Ihre Session.")

test_predefined_objects("Z", incorrect_msg = "Sie haben ein vordefiniertes Objekt manipuliert. Aktualisieren Sie Ihre Session.")

test_object("tstat", incorrect_msg = "Sie haben das Objekt falsch definiert.")

test_function("qt", args=c("p","df"), not_called_msg = "Sie haben die Quantilsfunktion der t-Verteilung nicht benutzt!")
test_or(
  {
    test_output_contains("T", incorrect_msg = "Sie haben keinen Vergleich mit logischen Operatoren durchgeführt!")
  },{
    test_output_contains("F", incorrect_msg = "Sie haben keinen Vergleich mit logischen Operatoren durchgeführt!")
  })



```

--- type:NormalExercise lang:r xp:100 skills:1 key:e319267621
## Heteroskedastie I

In der letzten Aufgabe sind Sie zu dem Schluss gekommen, dass der Koeffizient $\beta\_0$ im Regressionsmodell

$$ XP\_i = \beta\_0 + \beta\_1 \times Z\_i +  \epsilon\_i $$
  
  zum $5\%$-Niveau nicht signifikant von $0$ verschieden ist, wenn ein *nur bei Homoskedastie* konsistenter Standardfehler berechnet wird.

Betrachten Sie erneut den Plot: Eine weitere Auffälligkeit in den Daten ist, dass die Streuung der erreichten XP mit dem investierten Zeitaufwand zunimmt, d.h. es liegt Heteroskedastie vor.
<br>
  Sie sind besorgt über die Korrektheit der zuvor getroffenen Schlussfolgerung und wollen daher den Test mit heteroskedastie-robusten Standardfehlern wiederholen.

*Die Vektoren `XP` und `Z` sowie ein entsprechendes Regressionsmodell `mod` sind in Ihrer Arbeitsumgebung verfügbar.*
  
  
  *** =pre_exercise_code
```{r}
set.seed(2)
n <- 105
Z <- runif(n,0,24)
XP <- rep(NA,n)
for(i in 1:n) {
  XP[i] <- 100 + 60 * Z[i] + rnorm(1, sd=20*Z[i])
}
plot(Z,XP, pch=20, col="Steelblue", cex=0.5, xlim = c(0,24), ylim = c(0,1500), xlab="Zeitaufwand", ylab="XP")
mod <- lm(XP ~ Z)
```

***hint

Den White-Schätzer können Sie berechnen, indem Sie das Argument `type="HC0"` im Aufruf von `vcovHC` benutzen. Die Dimensionen einer Matrix können Sie mit `dim` überprüfen. 

***=instructions

- Laden Sie das Paket `sandwich`.
- Führen Sie zunächst eine Schätzung der Varianz-Kovarianz-Matrix der Regressionskoeffizienten mit dem Schätzer von <b>White</b> durch. Speichern Sie die Matrix in `hcm`. <b>Hinweis</b> Für Heteroskedastie robuste Schätzung der Varianz-Kovarianz-Matrix von Regressionskoeffizienten können Sie die Funktion `vcovHC` benutzen, s. `?vcovHC`. Beachten Sie das Argument `type`.
- Vergewissern Sie sich, dass es sich bei `hcm` um eine symmetrische $2\times 2$-Matrix handelt.

***=sample_code
```{r}
# Laden Sie das Paket sandwich


# Schätzen sie die Varianz-Kovarianz-Matrix


# Prüfen Sie die Dimensionen von hcm


```

***=solution
```{r}
# Laden Sie das Paket sandwich
library(sandwich)

# Schätzen sie die Varianz-Kovarianz-Matrix
mod <- lm(XP ~ Z)
hcm <- vcovHC(mod, type = "HC0")

# Prüfen Sie die Dimensionen von hcm
dim(hcm)

```

***=sct
```{r}
test_function("library", args = "package")

test_object("hcm", incorrect_msg = "Sie haben das Objekt falsch definiert.")

test_function("dim", args = "x")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:1e07ad71cf
## Heteroskedastie II

*Die Vektoren `XP` und `Z`, das Regressionsmodell `mod` sowie die geschätzte Varianz-Kovarianz-Matrix `hcm` sind in Ihrer Arbeitsumgebung verfügbar.*
  
  *** =pre_exercise_code
```{r}
library(sandwich)
library(lmtest)

set.seed(2)
n <- 105
Z <- runif(n,0,24)
XP <- rep(NA,n)
for(i in 1:n) {
  XP[i] <- 100 + 60 * Z[i] + rnorm(1, sd=20*Z[i])
}

mod <- lm(XP ~ Z)
hcm <- vcovHC(mod, type = "HC0")
```

***hint

`coeftest` besitzt das Argument `vcov.`. Die angegebene Matrix wird als Varianz-Kovarianz-Matrix zum Berechnen robuster Teststatistiken verwendet.
<br>
  Nützliche logische Operatoren sind `<` oder `>`. Die Länge eines Vektors bestimmen Sie mit `length`. $k$ ist die Anzahl der Regressoren im Modell. Bedenken Sie: Es handelt sich um einen beidseitigen Test, d.h. sie suchen einen kritischen Wert $c\_{1-\frac{\alpha}{2}}$.

***=instructions

- Laden Sie nun zusätzlich das Paket `lmtest`
- Führen Sie erneut einen Signifikanztest für $\beta\_0$ durch. Benutzen Sie dafür die Funktion `coeftest` in Kombination mit dem robusten Schätzer für die Varianz-Kovarianz-Matrix der geschätzten Koeffizienten aus der letzten Aufgabe 
- Speichern Sie die robuste $t$-Statistik in `tstat` und zeigen Sie mit logischen Operatoren, dass diese im Ablehnbereich für einen Test zum $5\%$-Niveau liegt und sich damit eine andere Schlussfolgerung als bei herkömmlichen Standardfehlern ergibt. 

***=sample_code
```{r}
# Laden Sie das Paket lmtest


# Benutzen Sie die Funktion coeftest


# Zeigen Sie, dass die robuste t-Statistik im Ablehnbereich liegt


```

***=solution
```{r}
# Laden Sie das Paket lmtest
library(lmtest)

# Benutzen Sie die Funktion coeftest und testen Sie erneut
mod <- lm(XP ~ Z)
tstat <- coeftest(mod, vcov.=hcm)[1,3]

# Zeigen Sie, dass die robuste t-Statistik im Ablehnbereich liegt
abs(tstat) >= qt(0.975, df = 103)
```

***=sct

```{r}
test_function("library")

test_function("coeftest")

test_object("tstat", incorrect_msg = "Sie haben das Objekt falsch definiert.")

test_function("qt", args=c("p","df"), not_called_msg = "Sie haben die Quantilsfunktion der t-Verteilung nicht benutzt!")
test_or(
  {
    test_output_contains("T", incorrect_msg = "Sie haben keinen Vergleich mit logischen Operatoren durchgeführt!")
  },{
    test_output_contains("F", incorrect_msg = "Sie haben keinen Vergleich mit logischen Operatoren durchgeführt!")
  })


```
--- type:NormalExercise lang:r xp:100 skills:1 key:726a6d460b
## Ein Linearer und Unverzerrter Schätzer?

Angenommen Sie betrachten das Regressionsmodel

$$ y\_i=\beta\_0 + \epsilon\_i \ \ , \ \ \epsilon\_i \sim (0,\sigma^2) \ \text{für} \ i=1,\dots,n $$
  
  d.h. eine Regression der Variable $\mathbf{Y} = (y\_1 \dots y\_n)$ auf einen konstanten Regressor $\mathbf{X} = (1 \dots 1)'.$

In `script.R` finden Sie eine Funktion, welche den OLS-Schätzer für $\beta\_0$ in diesem Modell berechnen soll. Allerdings ist die Funktion fehlerhaft programmiert: <br> Dieser Schätzer ist zwar linear aber *nicht unverzerrt* und entspricht nicht der OLS-Lösung.

*** =instructions

Passen Sie den Code der Funktion `OLS` im `script.R` an, sodass der OLS-Schätzer für $\beta\_0$ numerisch korrekt berechnet wird.

***=hint

Im obigen Modell lautet der OLS-Schätzer $\overline{Y} = \widehat{\beta}\_0 = \frac{1}{n} \sum\_{i=1}^n y_i$.

***=solution

```{r}
OLS <- function(Y) {
beta0 <- 1/length(Y)*sum(Y)
return(beta0)
} 
```

***=sample_code

```{r}
OLS <- function(Y) {
beta0 <- 1/length(Y)*sum(Y)+exp(mean(y))
return(beta0)
} 
```

*** =sct
```{r}
test_function_definition("OLS",
function_test = {
test_expression_result("OLS(seq(1,10,0.1))", incorrect_msg = "Die Funktion ist falsch definiert. Sie liefert nicht den passenden OLS-Schätzwert.")
},
undefined_msg = "Sie haben die Funktion `OLS` nicht definiert"
)
```

--- type:NormalExercise lang:r xp:200 skills:1 key:e95912639a
## Ein Linearer und Unverzerrter Schätzer! 

Betrachten Sie weiterhin das Regressionsmodell

$$ y\_i=\beta\_0 + \epsilon\_i \ \ , \ \ \epsilon\_i \sim (0,\sigma^2) \ \text{für} \ i=1,\dots,n $$

Aus der Vorlesung wissen Sie, dass ein Schätzer $\overset{\sim}{\beta}$ mit

$$ \overset{\sim}{\beta} = \sum\_{i=1}^n a\_i y\_i \ \ \text{und} \ \ \text{E}(\overset{\sim}{\beta}|X\_1,\dots, X\_n)=\beta $$

als linear und bedingt unverzerrt bezeichnet wird.
<br>
In dieser Aufgabe sollen Sie eine Schätzfunktion für $\beta\_0$ erstellen, deren Gewichte $a\_i$ von denen der OLS-Lösung abweichen, genauer

$$ \overset{\sim}{\beta}\_w = \sum\_{i=1}^n w\_i y\_i \ \ \text{wobei} \ \ w_i = \begin{cases}
\frac{1 + \epsilon}{n} & \text{wenn} \ i \leq \lfloor n/2 \rfloor \\\\ 1/n & \text{sonst.} \end{cases} $$

Weiterhin gelte $\epsilon = 0.8$.

$\lfloor x \rfloor$ ist die nächste ganze Zahl kleiner als x. 

***=hint

- Die Länge eines Vektors überprüfen Sie mit `length`

- Für $i > \lfloor n/2 \rfloor$ soll gelten $w\_i=1/n$. "Der zweite Teil" von `w` kann also erstellt werden, indem man `1/n` $n-\lfloor n/2 \rfloor$ mal erzeugt: 
`rep(1/n,ceiling(n/2))`. <br> Wie müssen Sie die ersten $\lfloor n/2 \rfloor$ Einträge erzeugen?

- Kombinieren Sie beide Teile mit `c()` um den Vektor `w` zu erzeugen.

*** =instructions
Betrachten Sie den vorgegebenen Code in `script.R`. Wie müssen Sie den Vektor der Gewichte `w` definieren? Ersetzen Sie `???` mit dem korrekten Ausdruck! <br><br> <b>Hinweise</b>: Benutzen Sie die Funktion `rep`, siehe `?rep`. Mit `floor` und `ceiling` können Sie ganzzahlig ab- bzw. aufrunden.


***=sample_code

```{r}

beta.w <- function(Y) {
n <- length(Y)
w <- ???
return(crossprod(w,Y)) # Skalarprodukt von w und Y
}

```

***=solution
```{r}
beta.w <- function(Y) {
n <- length(Y)
w <- c(rep((1+0.8)/n,floor(n/2)), rep(1/n,ceiling(n/2)))
return(crossprod(w,Y)) # Skalarprodukt von w und Y
}
```

*** =sct
```{r}
test_function_definition("beta.w",
function_test = {
test_expression_result("beta.w(seq(1,10,0.1))", incorrect_msg = "Die Funktion ist falsch definiert. Sie berechnet nicht den benötigten Schätzer.")
},
undefined_msg = "Sie haben die Funktion `beta.w` nicht definiert"
)
```

--- type:NormalExercise lang:r xp:200 skills:1 key:38065ff1c6
## Das Gauss-Markov-Theorem I

Erinnern Sie sich an die Aussage des Gauss-Markov-Theorems:
<br>
<br>
Sind die klassischen OLS-Annahmen erfüllt und die Fehlerterme homoskedastisch, so ist der OLS-Schätzer am effizientesten in der Klasse der linearen und bedingt unverzerrten Schätzer, d.h. es gibt keinen anderen qualifizierten Schätzer mit einer geringeren Varianz.

Sie sollen dies Anhand einer Simulationsstudie für die zuvor erstellten Schätzfunktionen `OLS` und `beta.w` verdeutlichen:

Die Simulation soll die folgenden Schritte umfassen:

1. Erstellen Sie einen Vektor `Y` mit $100$ Zufallszahlen aus einer $\mathcal{N}(0,1)$-Verteilung.
2. Berechnen Sie die Schätzer mit den Funktionen `OLS` und `beta.w`. Speichern Sie die Resultate jeweils an der $i$-ten Stelle der Vektoren `ols` und `weighted.w` ab.
3. Wiederholen Sie die Schritte 1. und 2. für $i=1,\dots,5000$.

<b>*Die Funktionen `OLS` und `beta.w` sind in ihrer Arbeitsumgebung verfügbar!*</b>

***=pre_exercise_code

```{r}
OLS <- function(Y) {
beta0 <- 1/length(Y)*sum(Y)
return(beta0)
} 

beta.w <- function(Y) {
n <- length(Y)
w <- c(rep((1+0.8)/n,floor(n/2)), rep(1/n,ceiling(n/2)))
return(crossprod(w,Y)) # Skalarprodukt von w und Y
}
```
***=hint

- Die Schleife muss `5000` mal durchlaufen
- Einen `n`-elementigen Vektor mit `NA`s initialisieren Sie durch `rep(NA,n)`
- Benutzen Sie die Funktionen `OLS` und `beta.w` um die Vektoren `ols` und `weighted.w` zu erzeugen

***=instructions
- Initialisieren Sie zunächst die Vektoren `ols` und `weighted.w`, sodass beide Vektoren $5000$ Einträge `NA` aufweisen.
- Ein Code-Gerüst für die obige Prozedur ist vorgegeben. Ersetzen Sie die `???` mit den korrekten Ausdrücken!

***=sample_code
```{r}
set.seed(1) # Für Sie nicht von Relevanz

# Initialisieren Sie die Vektoren ols und weighted.w


# Simulation
for (i in 1:???) {
y <- ???
ols[???] <- ???
weighted.w[???] <- ???
}
```

*** =solution

```{r}
set.seed(1) # Für Sie nicht von Relevanz

# Initialisieren Sie die Vektoren ols und weighted.w
ols <- rep(NA,5000)
weighted.w <- rep(NA,5000)

# Simulation
for (i in 1:5000) {
y <- rnorm(100)
ols[i] <- OLS(y)
weighted.w[i] <- beta.w(y)
}
```

***=sct

```{r}
test_student_typed("for (i in 1:5000)", not_typed_msg = "Benutzen Sie die vorgeschlagene for-Schleife!")
test_object("ols", eq_condition = "equal", incorrect_msg = "Sie haben das Objekt falsch definiert.")
test_object("weighted.w", eq_condition = "equal", incorrect_msg = "Sie haben das Objekt falsch definiert.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:86a8ca6d26
## Das Gauss-Markov-Theorem II

Betrachten Sie nun Ihre Ergebnisse aus der letzten Aufgabe genauer. 
Gemäß dem Gauss-Markov-Theorem können Sie erwarten, dass 
$$ \text{Var}(\widehat{\beta}\_{OLS}) < \text{Var}(\overset{\sim}{\beta}\_{w}). $$

`script.R` enthält einen Vorschlag, wie Sie dies grafisch veranschaulichen können.

*Die Vektoren `ols` und `weighted.w` aus der letzten Aufgabenstellung sind in ihrer Arbeitsumgebung verfügbar.*

<b>Hinweis</b>: *Beachten Sie, dass in der Konsole der Code für beide Histogramme gleichzeitig ausgeführt werden muss, ansonsten erhalten Sie eine Fehlermeldung!*

***=instructions
- Vervollständigen Sie die Befehle zum Erstellen der Histogramme.<br> <b>Hinweis</b>: Beide Histogramme sollen übereinander gezeichnet werden. Betrachten Sie `?hist` für weitere Details. Mit `col = alpha("red",0.6)` wird die Farbe Rot mit einem Deckungsgrad von $60\%$ gesetzt. 
- Berechnen Sie *ein* geeignetes Streuungsmaß für die simulierte Verteilung beider Punktschätzer und überprüfen Sie mit logischen Operatoren, ob Sie die obige Aussage des Gauss-Markov-Theorems bestätigen können.

***=hint

- Der zweite Aufruf von `hist` zeichnet das Histogramm für den Vektor `weighted.w`. Für welche Daten soll das erste Histogramm gezeichnet werden?
- Ein geeignetes Streuungsmaß ist die Varianz. Geeignete logische Operatoren sind `>` und `<`.

***=pre_exercise_code

```{r}
OLS <- function(Y) {
beta0 <- 1/length(Y)*sum(Y)
return(beta0)
} 

beta.w <- function(Y) {
n <- length(Y)
w <- c(rep((1+0.8)/n,floor(n/2)), rep(1/n,ceiling(n/2)))
return(crossprod(w,Y)) # Skalarprodukt von w und Y
}

ols <- rep(NA,5000)
weighted.w <- rep(NA,5000)



set.seed(1234)
for (i in 1:5000) {
y <- rnorm(100)
ols[i] <- OLS(y)
weighted.w[i] <- beta.w(y)
}
```

***=sample_code

```{r}
# Histogramme plotten
library(scales)
hist(x = ???, freq = F, col = ???, xlab = "OLS/Weighted")
hist(x = weighted.w, freq = F, add = ???, col = alpha("red",0.6))

# Streuungsmaße vergleichen


```

***=solution

```{r}
# Histogramme plotten
library(scales)
hist(x = ols, freq = F, col = "green")
hist(x = weighted.w, freq = F, add = T, col = alpha("red",0.6))

# Streuungsmaße vergleichen
sd(ols) > sd(weighted.w)
var(ols) > var(weighted.w)
```

***=sct

```{r}
test_function("hist", index = 1, args = "x")
test_function("hist", index = 2, args = c("x","add"))

test_or({
test_function("sd", index = 1)
test_function("sd", index = 2)
test_or({
test_student_typed("<")
},{
test_student_typed(">")
})
},{
test_function("var", index = 1)
test_function("var", index = 2)
test_or({
test_student_typed("<")
},{
test_student_typed(">")
})
})

test_or(
{
  test_output_contains("T", incorrect_msg = "Sie haben keinen Vergleich mit logischen Operatoren durchgeführt!")
},{
  test_output_contains("F", incorrect_msg = "Sie haben keinen Vergleich mit logischen Operatoren durchgeführt!")
}
)

```
