---
title       : Testat 1 WS 2017
description : 

---
## A1: California Test Score Data

```yaml
type: NormalExercise
key: 3fb3dd2f9a
lang: r
xp: 50
skills: 1
```

In diesem Testat sollen Sie Ihr Wissen bzgl. der Schätzung multipler Regressionsmodelle in <tt>R</tt> anwenden.

Die folgenden Aufgaben befassen sich mit der Frage, inwiefern das Verhältnis Anzahl Schüler / Anzahl Lehrer das Abschneiden der Schüler bei standardisierten Tests beeinflusst.

Sie arbeiten mit dem aus URFITE bekannten Datensatz `CASchools`. Dieser enthält enstprechende Daten für Grundschulen in Kalifornien.

`@instructions`

- Laden Sie das Paket `AER` sowie den Datensatz `CASchools`.

- Verschaffen Sie sich eine Übersicht über den Datensatz. 

<b>Hinweis</b>:
Nutzen Sie die `R`-Hilfe für Informationen zu den verfügbaren Variablen: `?CASchools`

`@hint`

- Pakete laden Sie mit `library()`. 
- Datensätze aus Paketen können mit `data()` in die Arbeitsumgebung geladen werden.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# Laden Sie das Paket


# Laden Sie den Datensatz


# Übersicht über CASchools 


```

`@solution`
```{r}
# Laden Sie das Paket
library(AER)

# Laden Sie den Datensatz
data(CASchools)

# Übersicht über CASchools 
summary(CASchools)
str(CASchools)
head(CASchools)
tail(CASchools)
```

`@sct`
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
    test_student_typed("data(CASchools, package = \"AER\")", not_typed_msg = "Funktion nicht oder falsch aufgerufen.")
})

test_or({
    test_function('summary',
                  not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
                  args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
                  incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
},{
    test_function('str',
                  not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
                  args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
                  incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
},{
    test_function('head',
                  not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
                  args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
                  incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
},{
    test_function('tail',
                  not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
                  args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
                  incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
})

test_function("data", 
              not_called_msg = "Funktion nicht oder falsch aufgerufen.", 
              args_not_specified_msg = "Funktion nicht oder falsch aufgerufen.",
              incorrect_msg = "Funktion nicht oder falsch aufgerufen.")

success_msg("Super!")
```


---
## A2: Variablen definieren

```yaml
type: NormalExercise
key: 1a32ab9189
lang: r
xp: 50
skills: 1
```

Zum Einstieg wollen Sie das Modell

$$ \texttt{score}\_i = \beta\_0 + \beta\_1 \times \texttt{STR}\_i + u\_i $$

schätzen. Hierzu müssen zunächst die Variablen <tt>score</tt> und <tt>STR</tt> folgendermaßen definiert werden:

$$ \texttt{score} = (\texttt{read} + \texttt{math}) / 2 $$

$$ \texttt{STR} = \texttt{students}/\texttt{teachers} $$

`@instructions`

- Definieren Sie <tt>score</tt> und <tt>STR</tt> wie oben angegeben.
- Weisen Sie die Ergebnisse den Variablen `score` und `STR` zu.

`@hint`

- Variablen in `CASchools` können mit dem `$`-Operator ausgelesen werden. 
- Verwenden Sie <tt>R</tt> als Taschenrechner und nutzen Sie den `<-` Operator, um die Ergebnisse `score` und `STR` zuzuweisen. 

`@pre_exercise_code`
```{r}
library(AER)                                                     
data(CASchools)
```

`@sample_code`
```{r}
# Score und STR definieren


```

`@solution`
```{r}
# Score und STR definieren
STR <- CASchools$students/CASchools$teachers
score <- (CASchools$read + CASchools$math)/2
```

`@sct`
```{r}
test_object("STR", incorrect_msg = "Das Objekt ist falsch definiert.", undefined_msg = "Objekt nicht definiert.")
test_object("score", incorrect_msg = "Das Objekt ist falsch definiert.", undefined_msg = "Objekt nicht definiert.")
success_msg("Super!")
```
---
## A3: Einfache Regression

```yaml
type: NormalExercise
key: d345364f21
lang: r
xp: 50
skills: 1
```
Die Vektoren `STR` und `score` aus der letzten Aufgabe wurden dem Datensatz `CASchools` hinzugefügt und können nun mit dem `$`-Operator ausgelesen werden.

Sie möchten nun folgendes Regressionsmodell für den Zusammenhang zwischen <tt>STR</tt> und <tt>score</tt>

$$ \texttt{score}\_i = \beta\_0 + \beta\_1 \times \texttt{STR}\_i + u\_i $$

schätzen.

`@instructions`

Schätzen Sie das Modell. Speichern Sie das geschätzte Modell in der Variable `mod1`. 

`@hint`

Lineare Modelle werden mit der Funktion `lm()` geschätzt. Siehe `?lm`.

`@pre_exercise_code`
```{r}
library(AER)                                                     
data(CASchools)
CASchools$STR <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$read + CASchools$math)/2   
```

`@sample_code`
```{r}
# Schätzen Sie das Modell

```

`@solution`
```{r}
# Schätzen Sie das Modell
mod1 <- lm(score ~ STR, data = CASchools)
```

`@sct`
```{r}
test_or({

test_function('lm', 
             args = c('formula', 'data'),
             not_called_msg = "Funktion nicht oder falsch aufgerufen.",
             args_not_specified_msg = "Funktion nicht oder falsch aufgerufen."
             )

},{

sol <- ex() %>% override_solution("mod1 <- lm(CASchools$score ~ CASchools$STR)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

fun <- ex() %>% override_solution('attach(CASchools); mod1 <- lm(score ~ STR)') 

fun %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.")  %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

fun %>% check_function('attach', not_called_msg = "Funktion nicht oder falsch aufgerufen.")

})

test_object('mod1', eval = F, undefined_msg = "Objekt nicht definiert.")

success_msg("Super!")
```

---
## A4: Robuste Standardfehler

```yaml
type: NormalExercise
key: 18570fb4bc
lang: r
xp: 200
skills: 1
```
Für das Regressionsmodell `mod1` aus der letzten Aufgabe kann mit `vcovHC()` eine robuste Schätzung der Kovarianzmatrix

$$
Var(\widehat{\beta}\_0,\widehat{\beta}\_1) =
\begin{pmatrix} 
    Var(\widehat{\beta}\_0) & Cov(\widehat{\beta}\_0,\widehat{\beta}\_1) \\\ \\\ 
    Cov(\widehat{\beta}\_0,\widehat{\beta}\_1) & Var(\widehat{\beta}\_1) 
\end{pmatrix}
$$

berechnet werden. Mit dieser Schätzung erhält man Standardfehler als

$$\sqrt{\widehat{Var}(\widehat{\beta}\_0)} = SE(\widehat{\beta}\_0)$$

und

$$\sqrt{\widehat{Var}(\widehat{\beta}\_1)} = SE(\widehat{\beta}\_1).$$

**`mod1` aus A3 ist in Ihrer Arbeitsumgebung verfügbar.**


`@instructions`

- Berechnen Sie zunächst mit `vcovHC()` eine robuste Schätzung der Kovarianzmatrix für $\widehat{\beta}\_0$ und $\widehat{\beta}\_1$ im Modell `mod1`. Speichern Sie das Ergebnis in `rob_cov`. 

- Berechnen Sie dann mithilfe von `rob_cov` robuste Standardfehler für beide Koeffizientenschätzer und speichern Sie diese in `SE0` und `SE1`.


`@hint`

- Einen Vektor mit den Diagonalelementen der Matrix `A` erhalten Sie mit `diag(A)`. 
- Das `i`-te Elemente aus dem Vektor `x` erhalten Sie mit `x[i]`.
- `sqrt(x)` berechnet die Wurzel von `x`.

`@pre_exercise_code`
```{r}
library(AER)  
library(lmtest)
data(CASchools)
CASchools$size <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$read + CASchools$math)/2
mod1 <- lm(score ~ size, data = CASchools)
```

`@sample_code`
```{r}
# Kovarianzmatrix robust schätzen


# Robuste Standardfehler berechnen


```

`@solution`
```{r}
# Kovarianzmatrix robust schätzen
rob_cov <- vcovHC(mod1)

# Robuste Standardfehler berechnen
SE0 <- sqrt(diag(rob_cov)[1])
SE1 <- sqrt(diag(rob_cov)[2])
```

`@sct`
```{r}

test_or({

    test_function('vcovHC',
                    args = 'x',
                    not_called_msg = "Funktion nicht oder falsch aufgerufen.",
                    args_not_specified_msg = "Funktion nicht oder falsch aufgerufen."
                 )

    test_object('rob_cov', incorrect_msg = "Objekt falsch definiert.", undefined_msg = "Objekt nicht definiert.")

},{

    sol <- ex() %>% override_solution('rob_cov <- hccm(mod1);SE0 <- sqrt(diag(rob_cov)[1]);SE1 <- sqrt(diag(rob_cov)[2])')
    sol %>% check_function('hccm') %>% check_arg('model', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    
},{
   
    fun <- ex() %>% override_solution('rob_cov <- vcovHC(mod1, type="HC1");SE0 <- sqrt(diag(rob_cov)[1]);SE1 <- sqrt(diag(rob_cov)[2])')
    fun %>% check_function('vcovHC') %>% check_arg('x', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    fun %>% check_function('vcovHC') %>% check_arg('type', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{
    fun <- ex() %>% override_solution('rob_cov <- vcovHC(mod1, type="HC0");SE0 <- sqrt(diag(rob_cov)[1]);SE1 <- sqrt(diag(rob_cov)[2])')
    fun %>% check_function('vcovHC') %>% check_arg('x', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
    fun %>% check_function('vcovHC') %>% check_arg('type', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")
})

test_object("SE0", eval=F)
test_object("SE1", eval=F)
test_object("rob_cov", eval=F)

success_msg("Super!")
```

---
## A5: Multiple Regression

Schulen mit großen Klassen liegen eher in sozial-schwachen Stadtteilen mit weniger Muttersprachlern. Vermutlich korreliert die Anzahl an Schülern pro Lehrer (<tt>STR</tt>) mit dem Anteil Englisch lernender Schüler in Prozent (<tt>english</tt>), sodass es einen omitted variable bias im einfachen Modell von Aufgabe 3 geben könnte. 

Sie möchten also das multiple Regressionsmodell

$$\texttt{score}\_i = \beta_0 + \beta\_1 \texttt{STR}\_i + \beta\_2 \times \texttt{english}\_i + u\_i$$

schätzen.

```yaml
type: NormalExercise
key: 753503bfdd
lang: r
xp: 100
skills: 1
```


`@instructions`

Schätzen Sie das obige multiple Regressionsmodell und speichern Sie das Resultat in `mod2`.

`@hint`

- Einfache und multiple lineare Regressionsmodelle können mit `lm()` geschätzt werden, siehe `?lm`. 
- Regressoren können im Argument `formula` einfach mit `+` hinzugefügt werden.

`@pre_exercise_code`
```{r}
library(AER)  
library(lmtest)
data(CASchools)
CASchools$STR <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$read + CASchools$math)/2
```

`@sample_code`
```{r}
# Schätzen Sie das multiple Modell


```

`@solution`
```{r}
# Schätzen Sie das multiple Modell
mod2 <- lm(score ~ STR + english, data = CASchools)
```

`@sct`
```{r}
test_or({

test_function('lm', 
             args = c('formula', 'data'),
             not_called_msg = "Funktion nicht oder falsch aufgerufen.",
             args_not_specified_msg = "Funktion nicht oder falsch aufgerufen."
             )
},{

sol <- ex() %>% override_solution("mod2 <- lm(CASchools$score ~ CASchools$STR + CASchools$english)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

fun <- ex() %>% override_solution('attach(CASchools); mod2 <- lm(score ~ STR + english)') 
fun %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.")  %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

})

test_object('mod2', eval = F, undefined_msg = "Objekt nicht definiert.")

success_msg("Super!")
```

---
## A6: Dummy-Variable erstellen

```yaml
type: NormalExercise
key: a019071e14
lang: r
xp: 100
skills: 1
```

`english` gibt den Anteil Englisch lernender Schüler **in Prozentpunkten** an.

Schulen mit mehr als $20\%$ Englischlernern gelten als besonders förderbedürftig. Zur Unterscheidung wird die Dummyvariable <tt>HiEL</tt> mit

$$\texttt{HiEL} = 
\begin{cases}
    1, \text{wenn} & \texttt{english} > 20\% \\\
    0, \text{sonst.}
\end{cases}$$

benötigt. Mit dem vorgegebenen Codeansatz soll <tt>HiEL</tt> erstellt und dem Datensatz hinzugefügt werden.

`@instructions`

Erstellen Sie die Dummyvariable <tt>HiEL</tt> wie oben angegeben.
Fügen Sie das Ergebnis zu `CASchools` hinzu, indem Sie `???` durch den gesuchten Code ersetzen.

`@hint`

Eine Dummyvariable kann nur die Werte `1` und `0` bzw. `TRUE` und `FALSE` annehmen.

Sei `a` der Vektor `(1,2,3,4)`:
- Der Befehl `a > 2` gibt den Vektor `c(FALSE, FALSE, TRUE, TRUE)` zurück. 
- Mit `as.numeric(a > 2)` erhält man den Vektor `c(0,0,1,1)`.

`@pre_exercise_code`
```{r}
library(AER)  
data(CASchools)
CASchools$STR <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$read + CASchools$math)/2
```

`@sample_code`
```{r}
# Vervollständigen Sie den Code
CASchools$HiEL <- ???
```

`@solution`
```{r}
# Vervollständigen Sie den Code
CASchools$HiEL <- CASchools$english > 20
```

`@sct`
```{r}
test_or({

test_object("CASchools", incorrect_msg = "Das Objekt ist falsch definiert.", undefined_msg = "Das Objekt ist falsch definiert.")

},{

ex() %>% override_solution("CASchools$HiEL <- as.numeric(CASchools$english > 20)") %>% check_function('as.numeric') %>% check_arg('x', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("CASchools$HiEL <- ifelse(CASchools$english > 20, 1, 0)") %>% check_function('ifelse') 
sol %>% check_arg('test') %>% check_equal("Funktion nicht oder falsch aufgerufen.")
sol %>% check_arg('yes') %>% check_equal("Funktion nicht oder falsch aufgerufen.")
sol %>% check_arg('no') %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("CASchools$HiEL <- ifelse(CASchools$english <= 20, 0, 1)") %>% check_function('ifelse') 
sol %>% check_arg('test') %>% check_equal("Funktion nicht oder falsch aufgerufen.")
sol %>% check_arg('yes') %>% check_equal("Funktion nicht oder falsch aufgerufen.")
sol %>% check_arg('no') %>% check_equal("Funktion nicht oder falsch aufgerufen.")

})


success_msg("Super!")
```

---
## A7: Regression mit Interaktionsterm

```yaml
type: NormalExercise
key: 441e2c6b93
lang: r
xp: 100
skills: 1
```

Sie vermuten, dass sich der Einfluss der Klassengröße (<tt>STR</tt>) auf das Testergebnis (<tt>score</tt>) für Klassen mit einem hohen Anteil an Englischlernern (<tt>HiEL=1</tt>) und solchen mit einem geringen Anteil (<tt>HiEL=0</tt>) unterscheidet.

Hierfür möchten Sie zunächst das folgende Modell mit *Interaktionsterm* schätzen:

$$ \texttt{score}\_i = \beta\_0 + \beta\_1 \texttt{STR}\_i + \beta\_2 \times \texttt{HiEL}\_i + \beta\_3 \times (\texttt{HiEL}\_i \times \texttt{STR}\_i) + u\_i$$


`@instructions`

- Schätzen Sie das obige Modell mit `lm()`.
- Speichern Sie das Ergebnis in `mod3`.

`@hint`

Es gibt zwei Möglichkeiten für Interaktion der Variablen `a` und `b` im Argument `formula` von `lm()`:

1. `a*b` fügt `a`, `b` und den Interaktionsterm  als Regressoren hinzu.  

2. `a:b` fügt nur den Interaktionsterm als Regressor hinzu.

`@pre_exercise_code`
```{r}
library(AER)  
data(CASchools)
CASchools$STR <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$read + CASchools$math)/2
CASchools$HiEL <- as.numeric(CASchools$english > 20)
```

`@sample_code`
```{r}
# Schätzen Sie das Regressionsmodell weisen Sie das Ergebnis mod3 zu

```

`@solution`
```{r}
# Schätzen Sie das Regressionsmodell weisen Sie das Ergebnis mod3 zu
mod3 <- lm(score ~ STR * HiEL, data = CASchools)
```

`@sct`
```{r}
test_or({

test_function('lm', 
             args = c('formula', 'data'),
             not_called_msg = "Funktion nicht oder falsch aufgerufen.",
             args_not_specified_msg = "Funktion nicht oder falsch aufgerufen."
             )
             

},{

sol <- ex() %>% override_solution("mod3 <- lm(CASchools$score ~ CASchools$STR + CASchools$HiEL + CASchools$STR:CASchools$HiEL)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("mod3 <- lm(CASchools$score ~ CASchools$STR + CASchools$HiEL + CASchools$HiEL:CASchools$STR)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

fun <- ex() %>% override_solution('attach(CASchools); mod3 <- lm(score ~ STR + HiEL + STR:HiEL)') 
fun %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.")  %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

fun <- ex() %>% override_solution('attach(CASchools); mod3 <- lm(score ~ STR + HiEL + HiEL:STR)') 
fun %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.")  %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

fun <- ex() %>% override_solution('attach(CASchools); mod3 <- lm(score ~ STR*HiEL)') 
fun %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.")  %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

fun <- ex() %>% override_solution('attach(CASchools); mod3 <- lm(score ~ HiEL*STR)') 
fun %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.")  %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

fun <- ex() %>% override_solution('attach(CASchools); mod3 <- lm(score ~ I(STR*HiEL))') 
fun %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.")  %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

fun <- ex() %>% override_solution('attach(CASchools); mod3 <- lm(score ~ I(HiEL*STR))') 
fun %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.")  %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("mod3 <- lm(score ~ I(STR*HiEL), data = CASchools)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("mod3 <- lm(score ~ I(HiEL*STR), data = CASchools)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("mod3 <- lm(score ~ STR + HiEL + STR:HiEL, data = CASchools)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("mod3 <- lm(score ~ STR + HiEL + HiEL:STR, data = CASchools)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("mod3 <- lm(CASchools$score ~ CASchools$STR*CASchools$HiEL)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("mod3 <- lm(CASchools$score ~ CASchools$HiEL*CASchools$STR)")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("mod3 <- lm(CASchools$score ~ I(CASchools$STR*CASchools$HiEL))")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

},{

sol <- ex() %>% override_solution("mod3 <- lm(CASchools$score ~ I(CASchools$HiEL*CASchools$STR))")
sol %>% check_function('lm', not_called_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_arg('formula', arg_not_specified_msg = "Funktion nicht oder falsch aufgerufen.") %>% check_equal("Funktion nicht oder falsch aufgerufen.")

})

test_object('mod3', eval = F)

success_msg("Super!")
```


---
## A8: Robuste Signifikanztests 

```yaml
type: NormalExercise
key: be9a9fa6d3
lang: r
xp: 100
skills: 1
```

$t$-Statistiken und $p$-Werten in `summary(mod3)$coefficients` darf bei Heteroskedastie nicht vertraut werden, da hier nur bei Homoskedastie gültige Standardfehler benutzt werden. 

Sie möchten bei Heteroskedastie gültige Signifikanztests durchführen.

**`mod3` aus A7 ist in Ihrer Arbeitsumgebung verfügbar.**


`@instructions`

Nutzen Sie eine Ihnen aus der Übung bekannte Funktion, um bei Heteroskedastie gültige Signifikanztests für die Koeffizienten in `mod3` durchzuführen.
<it>Der korrekte Aufruf dieser Funktion genügt, um die Aufgabe erfolgreich zu absolvieren!</it>

`@hint`

`coeftest()` gibt Koeffizienten und Ergebnisse von Signifikanztests für Modell-Objekte aus. Im Argument `vcov` kann eine Heteroskedastie-robuste Schätzung der Kovarianzmatrix übergeben werden. Schätzen Sie diese Matrix mit `vcovHC(mod3)`.

`@pre_exercise_code`
```{r}
library(AER)  
data(CASchools)
CASchools$STR <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$read + CASchools$math)/2
CASchools$HiEL <- as.numeric(CASchools$english > 20)
mod3 <- lm(score ~ STR + HiEL + STR * HiEL, data = CASchools)
```

`@sample_code`
```{r}
# Robuste Signifikanztests durchführen

```

`@solution`
```{r}
# Robuste Signifikanztests durchführen
coeftest(mod3, vcov = vcovHC(mod3))
```

`@sct`
```{r}
test_or({
    test_output_contains('coeftest(mod3, vcov = vcovHC(mod3))', incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
},{
    test_output_contains('coeftest(mod3, vcov = vcovHC(mod3, type="HC1"))', incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
},{
    test_output_contains('coeftest(mod3, vcov = vcovHC(mod3, type="HC0"))', incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
})
success_msg("Super!")
```
---
## A9: Robuster F-Test

```yaml
type: NormalExercise
key: 8bb55885be
lang: r
xp: 150
skills: 1
```

Das geschätzte Modell aus A7 ist

$$ \widehat{\texttt{score}}\_i = \underset{(10.85)}{691.67} \underset{(0.54)}{-1.59} \cdot \texttt{STR}\_i \underset{(20.16)}{-27.39} \cdot \texttt{HiEL}\_i + \underset{(1.00)}{0.26} \cdot (\texttt{STR}\_i \cdot \texttt{HiEL}\_i).$$

Sie vermuten, dass die Regressionsfunktion für Schulen mit hohem Anteil an Englischlernern (<tt>HiEL = 1</tt>) und solche mit niedrigem Anteil an Englischlernern (<tt>HiEL = 0</tt>) identisch ist.

**`mod3` aus A7 ist in Ihrer Arbeitsumgebung verfügbar.**

`@instructions`

Testen Sie die Hypothese, dass <tt>HiEL</tt> in diesem Modell keinerlei Einfluss hat. Nutzen Sie hierfür einen Heteroskedastie-robusten $F$-Test. 

<b>Hinweis</b>: Mit `linearHypothesis()` können lineare Restriktionen getestet werden.

Beachten Sie, dass der Interaktionsterm hier die Bezeichnung `STR:HiEL` hat.

`@hint`

- Wenn <tt>HiEL</tt> keinen Einfluss hat sind die Koeffizienten von <tt>HiEL</tt> und <tt>STR:HiSTR</tt> null.
- Verwenden Sie `vcov = vcovHC` in `linearHypothesis()`, um einen Heteroskedastie-robusten Test durchzuführen.

`@pre_exercise_code`
```{r}
library(AER)  
data(CASchools)
CASchools$STR <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$read + CASchools$math)/2
CASchools$HiEL <- as.numeric(CASchools$english > 20)
mod3 <- lm(score ~ STR + HiEL + STR:HiEL, data = CASchools)
```

`@sample_code`
```{r}
# Führen Sie den F-Test durch

```

`@solution`
```{r}
# Führen Sie den F-Test durch
linearHypothesis(mod3, c("HiEL=0","STR:HiEL=0"), vcov. = vcovHC(mod3))
```

`@sct`
```{r}

test_or({
    test_output_contains('linearHypothesis(mod3, c("HiEL=0","STR:HiEL=0"), vcov. = vcovHC(mod3))', incorrect_msg = "Funktion nicht oder falsch aufgerufen.")

},{

    test_output_contains('linearHypothesis(mod3, c("HiEL=0","STR:HiEL=0"), vcov. = vcovHC(mod3, type = "HC1"))', incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
    
},{
    
    test_output_contains('linearHypothesis(mod3, c("HiEL=0", "STR:HiEL=0"), vcov. = vcovHC(mod3, type = "HC0"))', incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
    
},{
    
    test_output_contains('linearHypothesis(mod3, c("STR:HiEL=0","HiEL=0"), vcov. = vcovHC(mod3))', incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
 
    
},{
    
    test_output_contains('linearHypothesis(mod3, c("STR:HiEL=0","HiEL=0"), vcov. = vcovHC(mod3, type = "HC1"))', incorrect_msg = "Funktion nicht oder falsch aufgerufen.")
    
},{
    
    test_output_contains('linearHypothesis(mod3, c("STR:HiEL=0","HiEL=0"), vcov. = vcovHC(mod3, type = "HC0"))', incorrect_msg = "Funktion nicht oder falsch aufgerufen.")    
})

success_msg("Super!")
```

---
## A10: Wald-Tests

```yaml
type: NormalExercise
key: 1433c45659
lang: r
xp: 100
skills: 1
```

$$q \cdot F = W$$ 
ist asymptotisch $\chi^2\_q$-verteilt, wobei $F$ die von `linearHypothesis()` standardmäßig berechnete $F$-Statistik unter Annahme von $q$ gemeinsam getesteten Hypothesen ist.

Ein (rechtsseitiger) Test anhand von $W$ ist asymptotisch äquivalent zum $F$-Test. Man nennt diese Tests auch *Wald-Tests*. 

In A9 sind $q=2$ Hypothesen gemeinsam zu testen. Nehmen Sie an die zugehörige $F$-Statistik beträgt $5$.

<b>Hinweis</b>: $\chi^2\_q$ meint die Chi-Quadrat-Verteilung mit $q$ Freiheitsgraden.

`@instructions`

- Berechnen Sie die Teststatistik $W$ und weisen Sie den Wert `W` zu.
- Berechnen Sie den $p$-Wert des Tests mit `pchisq()`, der Verteilungsfunktion der $\chi^2$-Verteilung. Weisen Sie den Wert der Variable `pval` zu.

`@hint`

- Es handelt sich um einen rechtsseitigen Hypothesentest, d.h. der $p$-Wert $P(W\geq 2\cdot 5) = 1 - P(W\leq 2\cdot 5)$ ist gesucht.

- In `pchisq()` muss neben der Teststatistik auch die Anzahl der Freiheitsgerade angegeben werden. Nutzen Sie die Hilfefunktion: `?pchisq`.

`@pre_exercise_code`
```{r}
library(AER)  
data(CASchools)
CASchools$STR <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$read + CASchools$math)/2
CASchools$HiEL <- as.numeric(CASchools$english > 20)
mod3 <- lm(score ~ STR + HiEL + STR * HiEL, data = CASchools)
```

`@sample_code`
```{r}
# Teststatistik und p-Wert berechnen


```

`@solution`
```{r}
# Teststatistik und p-Wert berechnen
W <- 2 * 5
pval <- 1 - pchisq(W, df = 2)
```

`@sct`
```{r}
test_predefined_objects("mod3")

test_object("W", incorrect_msg = "Objekt falsch definiert.", undefined_msg = "Objekt nicht definiert.")

test_object("pval", incorrect_msg = "Objekt falsch definiert.", undefined_msg = "Objekt nicht definiert.")

success_msg("Super!")
```
