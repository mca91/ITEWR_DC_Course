---
title       : Testat 1 WS 2017
description : 

--- type:NormalExercise lang:r xp:50 skills: key:79e6ade878
## A1: Paket und Datensatz

Ein für uns wichtiges <tt>R</tt>-Paket ist `AER` – *Applied Econometrics with R*. Es besteht aus vielen praktischen Funktionen und Datensätzen. 

In diesem Testat müssen Sie mit dem Datensatz `CPSSWEducation` arbeiten. Dieser ist ein Auszug des *Current Population Survey*, einer sozioökonomischen Umfrage in den USA und enthält Informationen zu Alter, Geschlecht, Einkommen sowie Bildungsgrad der Befragten. 

***=instructions
- Laden Sie das Paket <tt>AER</tt>.
- Laden Sie den Datensatz `CPSSWEducation` in Ihre Arbeitsumgebung.

***=hint
Mit der Funktion `data()` können verfügbare Datensätze in die Arbeitsumgebung geladen werden.

***=pre_exercise_code
```{r}
```

***=sample_code
```{r}
# Laden Sie das Paket


# Laden Sie den Datensatz


```

***=solution

```{r}
# Laden Sie das Paket
library(AER)
# Laden Sie den Datensatz
data(CPSSWEducation)
```

***=sct
```{r}
test_or({
    test_student_typed("library(AER)", not_typed_msg = "Funktion nicht oder falsch aufgerufen.")
},{
    test_student_typed("require(AER)", not_typed_msg = "Funktion nicht oder falsch aufgerufen.")
},{    
    test_student_typed("library(\"AER\")", not_typed_msg = "Funktion nicht oder falsch aufgerufen.")
},{
    test_student_typed("require(\"AER\")", not_typed_msg = "Funktion nicht oder falsch aufgerufen.")
},{
    test_student_typed("data(CPSSWEducation, package = \"AER\")", not_typed_msg = "Funktion nicht oder falsch aufgerufen.")
})
test_function("data", 
              not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
              args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
              incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
success_msg("Richtig!")
```

--- type:NormalExercise lang:r xp:50 skills:1 key:23031eeba9
## A2: Ein Erster Überblick

*Der Datensatz `CPSSWEducation` ist in der Arbeitsumgebung verfügbar.*

*** =instructions

- Speichern Sie den Datensatz unter der Variable `daten`.
- Verschaffen Sie sich einen Überblick über den Datensatz.
- Berechnen Sie die Stichprobenvarianz für die Variablen `earnings` und `education`.

*** =hint

- Einen Überblick verschaffen Sie sich mit `summary()`.   
- `sd()` berechnet die Stichprobenstandardabweichung. 
- Der `$`-Operator kann nützlich sein.

*** =pre_exercise_code
```{r}
library(AER)
data(CPSSWEducation)
```

*** =sample_code
```{r}
# Datensatz unter 'daten' speichern


# Überblick verschaffen


# Stichprobenvarianzen berechnen
var_earnings <- ???
var_education <- ???
```

*** =solution
```{r}
# Datensatz unter 'daten' speichern
daten <- CPSSWEducation

## Überblick verschaffen
summary(daten)

# alternativ
str(daten)
head(daten)

# Stichprobenvarianzen berechnen
var_earnings <- var(daten$earnings)
var_education <- var(daten$education)
```

*** =sct
```{r}
test_object("daten", incorrect_msg = "Das Objekt ist falsch definiert.")

test_or(
    test_function("summary", args="object", 
                  not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
                  args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
                  incorrect_msg = "Funktion nicht oder falsch aufgerufen."),
    test_function("head", args="x", 
                  not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
                  args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
                  incorrect_msg = "Funktion nicht oder falsch aufgerufen."),
    test_function("str", args="object", 
                  not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
                  args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
                  incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
)

test_object("var_earnings", incorrect_msg = "Das Objekt ist falsch definiert.")
test_object("var_education", incorrect_msg = "Das Objekt ist falsch definiert.")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:f21819423a
## A3: Beobachtungen Plotten

*Das Objekt `daten` aus der letzten Aufgabe ist in der Arbeitsumgebung verfügbar.*

Als Studierende*r der Volkswirtschaftslehre interessieren Sie sich für den Zusammenhang zwischen Einkommen und Bildung.

*** =instructions

- Stellen Sie die Beobachtungen grafisch dar indem Sie `education` gegen `earnings` plotten.
- Berechnen Sie ein geeignetes Maß für die Stärke des linearen Zusammenhangs zwischen `education` und `earnings`. Speichern Sie dieses in der Variable `Cor`.

*** =hint
- Verwenden Sie die Funktion `plot()`. 
- Ein geeignetes Maß ist der Korrelationskoeffizient, siehe `?cor`.

*** =pre_exercise_code
```{r}
library(AER)
data(CPSSWEducation)
daten <- CPSSWEducation
```

*** =sample_code
```{r}
# Plotten Sie die Beobachtungen


# Linearen Zusammenhang messen


```

*** =solution
```{r}
# Plotten Sie die Beobachtungen
plot(daten$education, daten$earnings)

# Linearen Zusammenhang messen
Cor <- cor(daten$education, daten$earnings)
```

*** =sct
```{r}
test_object("daten", incorrect_msg = "Das Objekt ist falsch definiert.")

test_or({
  fun <- ex() %>% check_function('plot', not_called_msg = "Funktion nicht oder falsch aufgerufen.")
  fun %>% check_arg('x', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
  fun %>% check_arg('y', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
}, {
  fun <- ex() %>% override_solution('plot(earnings ~ education, data = daten)') %>% check_function('plot', not_called_msg = "Funktion nicht oder falsch aufgerufen.")
  fun %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
  fun %>% check_arg('data', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
}, {
  ex() %>% override_solution('plot(daten$earnings ~ daten$education)') %>% check_function('plot', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
}, {
  ex() %>% override_solution('attach(daten);plot(earnings ~ education)') %>% check_function('plot', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
})

test_object('Cor', incorrect_msg = "Das Objekt ist falsch definiert.")

success_msg("Richtig, weiter so!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:ef378dde98
## A4: Ein Lineares Modell

*Das Objekt `daten` ist in der Arbeitsumgebung verfügbar.*

Sie vermuten, dass der Zusammenhang durch das einfache lineare Regressionsmodell $$earnings\_i = \beta\_0 + \beta\_1 \times education\_i + u\_i$$ beschrieben werden kann.

*** =instructions

- Schätzen Sie das obige Modell mit einer geeigneten R-Funktion, die Sie aus der Übung kennen. Speichern Sie das Resultat in `mod`.
- Lassen Sie sich eine Zusammenfassung des Modellobjekts `mod` anzeigen.

*** =hint
- Lineare Regressionsmodelle können mit der Funktion `lm()` geschätzt werden. Eine einfache Regression von `a` auf `b` führen Sie mit `lm(a ~ b)` durch. 
- Eine Zusammenfassung von Objekten erhalten Sie mit `summary()`.

*** =pre_exercise_code
```{r}
library(AER)
data(CPSSWEducation)
daten <- CPSSWEducation
```

*** =sample_code
```{r}
# Schätzen Sie das Regressionsmodell


# Statistische Informationen erhalten


```

*** =solution
```{r}
# Schätzen Sie das Regressionsmodell
mod <- lm(earnings ~ education, data = daten)

# Statistische Informationen erhalten
summary(mod)
```

*** =sct
```{r}
test_or({
ex() %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
ex() %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('data', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
},{
sol <- ex() %>% override_solution("mod <- lm(daten$earnings ~ daten$education)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
},{
fun <- ex() %>% override_solution('attach(daten); mod <- lm(earnings ~ education)') 
fun %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.")  %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
})

ex() %>% check_object('mod')

ex() %>% override_solution('mod <- lm(daten$earnings ~ daten$education); summary(mod)') %>% check_output_expr('summary(mod)', missing_msg = "Funktion nicht oder falsch aufgerufen.")

success_msg("Super!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:85642fd5e1
## A5: Anpassungsgüte

$R^2$ und $SER$ sind Maße der Anpassungsgüte eines Regressionsmodells an die beobachteten Daten. 

$$R^2 = \frac{ESS}{TSS} = 1 - \frac{SSR}{TSS},$$

$$SER=\sqrt{\frac{1}{n-k-1}\sum\_{i=1}^n \widehat{u}^2\_i} = \sqrt{\frac{1}{n-k-1} SSR}$$

**Hinweis:** Es gibt einen einfacheren Weg als die Formeln zu benutzen.

**Das Objekt `mod` aus A4 und der Datensatz `daten` sind in Ihrer Arbeitsumgebung verfügbar.**


*** =instructions

Berechnen Sie $SSR$, $R$ und $SER$ für das in `mod` gespeicherte Regressionsmodell. Weisen Sie die Werte den Variablen `SSR`, `R2` und `SER` zu.

*** =hint

- Das Objekt `mod` enthält die Residuen der Regression: `mod$residuals`. Somit kann `SSR` berechnet werden.  
- `R2` und `SER` können mit `summary()` ausgelesen werden. Nutzen Sie den `$`-Operator.

*** =pre_exercise_code
```{r}
library(AER)
data(CPSSWEducation)
daten <- CPSSWEducation
mod <- lm(earnings ~ education, data = CPSSWEducation)
```

*** =sample_code
```{r}
# Berechnen Sie SSR, R2 und SER 


```

*** =solution
```{r}
# Berechnen Sie SSR, R2 und SER 
SSR <- sum(mod$res^2)
R2 <- summary(mod)$r.squared
SER <- summary(mod)$sigma
```

*** =sct
```{r}
test_predefined_objects('mod', incorrect_msg = "Das Objekt ist falsch definiert.")
test_object('SSR', incorrect_msg = "Das Objekt ist falsch definiert.")
test_object('R2', incorrect_msg = "Das Objekt ist falsch definiert.")
test_object('SER', incorrect_msg = "Das Objekt ist falsch definiert.")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:0568f097e5
## A6: Konfidenzintervalle

Das in `mod` gespeicherte, geschätzte Modell aus A4 lautet

$$ \widehat{earnings}\_i = \underset{(0.95925)}{-3.134} + \underset{(0.06978)}{1.467} \times education_i. $$

**Das Objekt `mod` ist in Ihrer Arbeitsumgebung verfügbar.**

*** =instructions

Nutzen Sie eine Ihnen aus der Übung bekannte Funktion, um $99\%$-Konfidenzintervalle für die Konstante sowie den Koeffizienten von $education$ zu berechnen.

*** =hint

`confint()` berechnet Konfidenzintervalle für Koeffizienten von linearen Modellen. Beachten Sie, dass das Konfidenzlevel $99\%$ betragen soll!

*** =pre_exercise_code
```{r}
library(AER)
data(CPSSWEducation)
mod <- lm(earnings ~ education, data = CPSSWEducation)
```

*** =sample_code
```{r}
# Konfidenzintervalle berechnen

```

*** =solution
```{r}
# Konfidenzintervalle berechnen
confint(mod, level = 0.99)
```

*** =sct
```{r}
test_predefined_objects('mod', incorrect_msg = "Das Objekt ist falsch definiert.")

test_or({
    sol <- ex() %>% check_function('confint', not_called_msg = "Funktion nicht oder falsch aufgerufen.") 
    sol %>% check_result() %>% check_equal()
},{
    sol1 <- ex() %>% override_solution('confint(mod, parm = "education", level = 0.99)') %>% check_function('confint', not_called_msg = "Funktion nicht oder falsch aufgerufen.") 
    
    sol1 %>% check_arg('object', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
    sol1 %>% check_arg('parm', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
    sol1 %>% check_arg('level', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
    sol2 <- ex() %>% override_solution('confint(mod, parm = "(Intercept)", level = 0.99)') %>% check_function('confint', not_called_msg = "Funktion nicht oder falsch aufgerufen.")
    
    sol2 %>% check_arg('object', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
    sol2 %>% check_arg('parm', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
    sol2 %>% check_arg('level', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
},{
    sol1 <- ex() %>% override_solution('confint(mod, parm = 1, level = 0.99)') %>% check_function('confint', not_called_msg = "Funktion nicht oder falsch aufgerufen.") 
    
    sol1 %>% check_arg('object', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
    sol1 %>% check_arg('parm', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
    sol1 %>% check_arg('level', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
    sol2 <- ex() %>% override_solution('confint(mod, parm = 2, level = 0.99)') %>% check_function('confint', not_called_msg = "Funktion nicht oder falsch aufgerufen.")
    
    sol2 %>% check_arg('object', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
    sol2 %>% check_arg('parm', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
    sol2 %>% check_arg('level', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
})

success_msg("Super!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:89caadc354
## A7: Hypothesentest I

Bei Heteroskedastie sind herkömmliche $t$-Statistiken und Konfidenzintervalle ungültig. 
Unter Verwendung robuster Standardfehler erhält man

$$ \widehat{earnings}\_i = \underset{(0.9268)}{-3.134} + \underset{(0.0720)}{1.467} \times education_i. $$

Sie vermuten, dass ein zusätzliches Jahr Bildung zu einem erwarteten Anstieg des Stundenlohns von $\$1$ führt.

Sie wählen das Signifikanzniveau $\alpha = 0.05$.

**Das Objekt `mod` aus der letzten Aufgabe ist in Ihrer Arbeitsumgebung verfügbar. $SE(\widehat\beta_1)$, der robuste Standardfehler für $\widehat\beta\_1$ ist unter `se` gespeichert.**

*** =instructions

Berechnen Sie die im Code vorgegebenen Größen **mit R** und weisen Sie diese den Variablen zu. Nutzen Sie hierfür `summary()`.

Formeln: $t = \frac{\widehat{\beta}\_1 - \beta\_{1,0}}{SE(\widehat{\beta}\_1)} \ \ , \ \ p\text{-Wert}= 2 \cdot [1-\Phi(|t\_{act}|)]$

*** =hint

Folgende Funktionen können hilfreich sein:

`summary()`,`coef()`, `abs()`, `pnorm()`

*** =pre_exercise_code
```{r}
library(AER)
library(lmtest)
data(CPSSWEducation)
mod <- lm(earnings ~ education, data = CPSSWEducation)
robvcov <- vcovHC(mod)
se <- sqrt(robvcov[2,2])
```

*** =sample_code
```{r}
# Schätzwert für beta_1:
beta_1_dach <- ???

# Nullhypothese:
beta_10 <- ???

# Teststatistik:
t_act <- ???

# p-Wert:
p_wert <- ???
```

*** =solution
```{r}
# Schätzwert für beta_1:
beta_1_dach <- coef(mod)[2]

# Nullhypothese:
beta_10 <- 1

# Teststatistik:
t_act <- (beta_1_dach - beta_10)/se

# p-Wert:
p_wert <- 2*(1-pnorm(abs(t_act)))
```

*** =sct
```{r}
test_predefined_objects('mod', incorrect_msg = "Das Objekt ist falsch definiert.")
test_predefined_objects('se', incorrect_msg = "Das Objekt ist falsch definiert.")


test_object("beta_1_dach", incorrect_msg = "Das Objekt ist falsch definiert.")
test_object("beta_10", incorrect_msg = "Das Objekt ist falsch definiert.")
test_object("t_act", incorrect_msg = "Das Objekt ist falsch definiert.")
test_object("p_wert", incorrect_msg = "Das Objekt ist falsch definiert.")

success_msg("Super!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:b5af0398c0
## A8: Hypothesentest II

Nehmen Sie an, der $p$-Wert (`p_wert`) zum Hypothesentest $H_0: \beta\_1 = 1$ aus der vorherigen Aufgabe beträgt $1.1\cdot 10^{-11}$. 

*** =instructions

- Weisen Sie den Variablen die korrekten Werte zu.
- Nutzen Sie logische Operatoren um zu überprüfen, ob die Nullhypothese zum Niveau $\alpha=0.05$ abgelehnt oder belassen wird.

*** =hint

Logische Operatoren in <tt>R</tt> sind bspw. `&`,`|`,`<`,`>`,`==`,`<=` und `>=`.

*** =pre_exercise_code
```{r}
```

*** =sample_code
```{r}
# p_wert und Signifikanzniveau zuweisen
p_wert <- ???
alpha <- ???

# p_wert und Signifikanzniveau vergleichen

```

*** =solution
```{r}
# p_wert und Signifikanzniveau zuweisen
p_wert <- 1.1*10^(-11)
alpha <- 0.05

# Mit Signifikanzniveau vergleichen
p_wert <= alpha
```

*** =sct
```{r}
test_object('p_wert', incorrect_msg = "Das Objekt ist falsch definiert.")
test_object('alpha', incorrect_msg = "Das Objekt ist falsch definiert.")

test_or(
    test_student_typed('p_wert <= alpha', not_typed_msg = "Funktion nicht oder falsch aufgerufen."),
    test_student_typed('alpha <= p_wert', not_typed_msg = "Funktion nicht oder falsch aufgerufen."),
    test_student_typed('p_wert >= alpha', not_typed_msg = "Funktion nicht oder falsch aufgerufen."),
    test_student_typed('alpha >= p_wert', not_typed_msg = "Funktion nicht oder falsch aufgerufen."),
    
    test_student_typed('p_wert < alpha', not_typed_msg = "Funktion nicht oder falsch aufgerufen."),
    test_student_typed('alpha < p_wert', not_typed_msg = "Funktion nicht oder falsch aufgerufen."),
    test_student_typed('p_wert > alpha', not_typed_msg = "Funktion nicht oder falsch aufgerufen."),
    test_student_typed('alpha > p_wert', not_typed_msg = "Funktion nicht oder falsch aufgerufen.")
    
)

success_msg("Korrekt!")
```




--- type:NormalExercise lang:r xp:150 skills:1 key:53ae8b672c
## A9: Regression ohne Konstante

Betrachten Sie nun das allgemeine Modell $$Y\_i = \beta\_1 X\_i + u\_i.$$ 

Der KQ-Schätzer für $\beta\_1$ lautet hier $$\widehat{\beta}\_1 = \frac{\sum_{i=1}^n Y\_i X\_i }{\sum\_{i=1}^n X\_i^2}.$$

Im R-Skript finden Sie eine Funktion, welche $\widehat{\beta}_1$ für zwei Vektoren gleicher Länge auf vier Nachkommastellen genau berechnen soll. Leider sind Teile des Codes verloren gegangen.

**Hinweis:** `round(x, 2)` rundet `x` auf zwei Nachkommastellen.

*** =instructions

Vervollständigen Sie die Funktion, indem Sie mit `???` gekenzeichnete Passagen mit den richtigen Befehlen ersetzen.

*** =hint

Das Skalarprodukt von zwei Vektoren `a` und `b` berechnet man mit `a %*% b`.

*** =pre_exercise_code
```{r}
library(AER)
data(CPSSWEducation)
```

*** =sample_code
```{r}
# Vervollständigen Sie den Code

regression <- function(X, Y) {
  
  if(length(X) != length(Y)) break
  
  beta_1_hat <- ???
  
  return(
    c(round(beta_1_hat, ???))
  )
}
```

*** =solution
```{r}
# Vervollständigen Sie den Code
regression <- function(X, Y) {
  if(length(X) != length(Y)) break
  beta_1_hat <- X %*% Y / X %*% X
    return(
      c(round(beta_1_hat, 4))
    )
}
```

*** =sct
```{r}
test_function_definition("regression",
    
    function_test = test_expression_result("regression(CPSSWEducation$education, CPSSWEducation$earnings)"),
    
    body_test = {
    
        test_function("length", index = 1,
                      not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
                      args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
                      incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
                      
        test_function("length", index = 2, 
                      not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
                      args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
                      incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
                      
        test_function("round", args = "digits", 
              not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
              args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
              incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
    }
)
```

--- type:NormalExercise lang:r xp:150 skills:1 key:9e85e20cb6
## A10: Simulation

Betrachten Sie nun das Modell 
$$ Y\_i = \beta+ u\_i. $$ 

$\widehat{\beta}$, der KQ-Schätzer für $\beta$ in diesem Modell ist aus der Übung bekannt.

Sei $Y\_i \overset{i.i.d.}{\sim} \mathcal{N}(\mu=5,\sigma^2=25)$.

*** =instructions

Nutzen Sie die Funktion `replicate()` um $1000$ mal den KQ-Schätzer von $\beta$ für Zufallsstichproben mit je $100$ Beobachtungen zu berechnen. Speichern Sie die Ergebnisse im Vektor `beta_hats`.

*** =hint

- $\widehat{\beta} = \frac{1}{n} \sum\_{i=1}^n Y\_i$, der Mittelwert der $Y_i$ ist der KQ-Schätzer für $\beta$ im obigen Modell.
- Hilfreiche Funktionen sind `mean()` und `rnorm()`.

*** =pre_exercise_code
```{r}
custom_seed(1)
```

*** =sample_code
```{r}
# Simulieren Sie 1000 Schätzvorgänge


```

*** =solution
```{r}
# Simulieren Sie 1000 Schätzvorgänge
beta_hats <- replicate(1000, mean(rnorm(100,5,5)))
```

*** =sct
```{r}
test_object('beta_hats', incorrect_msg = "Das Objekt ist falsch definiert.")
test_function('replicate', 
              not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
              args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
              incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
```


