---
title       : Mock Exam I
description : Dieses Testat besteht aus einem Kapitel mit insgesamt 11 Aufgaben. Die Aufgaben können unabhängig voneinander gelöst werden.

--- type:NormalExercise lang:r xp:100 skills: key:e8803615c1
## A1 Importieren eines Datensatzes in R

In dieser Aufgabe sollen Sie eine .csv-Datei einlesen.

Die Datei *cps_ch3.csv* enthält einen Auszug des Current Population Survey, einer sozioökonomischen Umfrage in den USA.<br> <b>*Der Datensatz ist online unter der im R-Skript angegebenen Web-Adresse verfügbar.*</b>
  
*** =instructions
Lesen Sie den oben ganannten Datensatz *adäquat* ein und weisen Sie das Resultat dem Objekt `cps` zu.<br><br> <b>Hinweis:</b> Sie können die Web-Adresse als Pfad-Argument in der gesuchten Funktion nutzen!
  
*** =sample_code
```{r}
# Lesen Sie den Datensatz ein und nennen Sie das Object cps.
# URL: http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv


```

*** =hint

Benutzen Sie die Funktion `read.table` zum Einlesen der Daten. Nutzen Sie die Argumente `header` und `sep`. Mit welchem Symbol sind Beobachtungen unterschiedlicher Variablen im Datensatz separiert?

*** =solution
```{r}
# Lesen Sie den Datensatz ein und nennen Sie das Object cps.
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
```

*** =sct
```{r}
test_or({
  test_object("cps", undefined_msg = "Sie haben das Objekt `cps` nicht erstellt.", incorrect_msg = "Das Objekt `cps` ist falsch definiert.")
},{
  ex() %>% override_solution('cps <- read.csv2("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv")') %>% check_object('cps') %>% check_equal(incorrect_msg = "Das Objekt `cps` ist falsch definiert.", undefined_msg = "Sie haben das Objekt `cps` nicht erstellt.")
})
success_msg("Weiter so!")
```

--- type:NormalExercise lang:r xp:100 skills: key:1152cc1eba
## A2 Beobachtungen anzeigen

*Der Datensatz `cps` aus der vorherigen Aufgabe ist in Ihrer Arbeitsumgebung verfügbar!*
  
  
*** =pre_exercise_code
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
```

*** =instructions
- Aus der Übung kennen Sie Möglichkeiten, die ersten `n` Reihen eines Objekts auszulesen. Lassen Sie sich die ersten 10 Beobachtungen der Tabelle `cps` anzeigen!

*** =hint
Eine geeignete Funktion zum Anzeigen der ersten paar Beobachtungen ist `head`. Für weitere Hilfestellung, nutzen Sie die Hilfefunktion, indem Sie `?head` über die Konsole aufrufen.

*** =sample_code
```{r}
# Lassen Sie sich die ersten 10 Beobachtungen des Datensatzes anzeigen.


```

*** =solution
```{r}
# Lassen Sie sich die ersten 10 Beobachtungen des Datensatzes anzeigen.
head(cps, n=10) 
```

*** =sct
```{r}
test_or({
  test_student_typed("cps[1:10,]", not_typed_msg = "Sie haben nicht die gewünschten Zeilen ausgelesen.")
},{
  test_function("head", args = "n", args_not_specified_msg = "Ein notwendiges Argument wurde nicht angegeben.", incorrect_msg = "Etwas ist falsch...")
})
success_msg("Weiter so!")
```
--- type:NormalExercise lang:r xp:100 skills: key:d0b5af7a21
## A3 Deskriptive Statistiken

*Der Datensatz `cps` aus der vorherigen Aufgabe ist in Ihrer Arbeitsumgebung verfügbar!*
  
*** =pre_exercise_code
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
```

*** =instructions
- Verschaffen Sie sich einen Überblick über den Datensatz mit einer aus der Übung bekannten Funktion.

*** =hint
Einen Überblick verschaffen Sie sich mit der Funktion `summary`.

*** =sample_code
```{r}
# Verschaffen Sie sich einen Überblick über den Datensatz.



```

*** =solution

```{r}
# Verschaffen Sie sich einen Überblick über den Datensatz.
summary(cps)
```

*** =sct

```{r}
test_predefined_objects("cps")
test_function("summary", args="object", incorrect_msg = "Sie haben die Funktion auf ein falsches Objekt angewendet!")
success_msg("Weiter so!")
```

--- type:NormalExercise lang:r xp:200 skills: key:99a5fdcf85
## A4 Ein bearbeiteter Datensatz

*Der Datensatz `cps` aus der vorherigen Aufgabe ist in Ihrer Arbeitsumgebung verfügbar!*
  
*** =pre_exercise_code
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
```

*** =instructions
- Erstellen Sie eine Kopie von `cps` namens `cps.neu`. 
- Sollten Sie alles richtig gemacht habe, so ist `cps.neu` mit `cps` identisch. `cps.neu` ist also ebenfalls ein Objekt vom Typ `data.frame`. Ändern Sie die Namen der Variablen -- d.h. die Spaltennamen -- in `cps.neu` wie folgt:
  * `a_sex` zu `Geschlecht`
  * `year` zu `Jahr`
  * `ahe12` zu `Stundenlohn`

*** =hint
- Erstellen Sie die Kopie `cps.neu` mithilfe des Operators `<-`. Was müssen Sie `cps.neu` zuweisen?
- Spaltennamen eines `data.frame`-Objekts wie `cps.neu` können Sie mithilfe der Funktion `colnames` auslesen und überschreiben. Betrachten Sie `?colnames` für weitere Hinweise.

*** =sample_code
```{r}
# Erstellen Sie die Kopie.


# Ändern Sie die namen der Variablen in cps.neu.


```

*** =solution
```{r}
# Erstellen Sie die Kopie und ändern Sie die Variablennamen.
cps.neu <- cps
names(cps.neu) <- c("Geschlecht","Jahr","Stundenlohn")

```

*** =sct
```{r}
test_predefined_objects("cps")
test_object("cps.neu", eq_condition = "equal",undefined_msg = "Sie haben das Objekt `cps.neu` nicht erstellt.", incorrect_msg = "Das Objekt `cps.neu` ist falsch definiert.")
success_msg("Weiter so!")
```

--- type:NormalExercise lang:r xp:200 skills: key:812718ebe3
## A5 Ändern der Kodierung von Variablen

*Der Datensatz `cps.neu` aus der vorherigen Aufgabe ist in Ihrer Arbeitsumgebung verfügbar!*
  
*** =pre_exercise_code
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
cps.neu <- cps
names(cps.neu) <- c("Geschlecht","Jahr","Stundenlohn")
```

*** =instructions
- Ändern Sie die Kodierung der Spalte `Geschlecht` <b>im Datensatz cps.neu</b> so, dass für alle Beobachtungen mit `Geschlecht==2` (für weiblich) anschließend `Geschlecht==0` ist.<br><br> Vervollständigen Sie hierzu zunächst den vorgegebenen Aufruf von `replace` und passen Sie dann `cps.neu` an.<br><b>Hinweis</b>: Siehe `?replace`. Ein Index-Vektor kennzeichnet Elemente, für die eine bestimmte Eigenschaft zutrifft. Wie können Sie diesen Vektor erhalten?<br><br>
  - Vergessen Sie nicht, vor dem Abschicken der Lösung `#` zu entfernen!
  
*** =hint
- Mit dem Operator `==` kann man die Identität von Objekten prüfen. Beispielsweise erhalten Sie mit `c(1,2,3)==1` einen logischen Vektor mit den Komponenten `TRUE` oder `FALSE`. Die Einträge dieses Vektors geben an, ob die jeweiligen Elemente von `c(1,2,3)` den Wert `1` haben. Probieren Sie es selber einmal aus!
  <br><br>
  Was müssen Sie gemäß der Aufgabenstellung überprüfen?
<br><br>
  - Überschreiben Sie die Spalte `Geschlecht` in `cps.neu` mit dem Ergebnis aus dem Aufruf von `replace`. Hierzu verwenden Sie den Operator `<-`.

*** =sample_code
```{r}
# Ändern Sie die Kodierung für "Geschlecht" im Object `cps.neu
# replace(cps.neu$Geschlecht, list =    , values = 0)
```

*** =solution
```{r}
# Ändern Sie die Kodierung für "Geschlecht" im Object `cps.neu
cps.neu$Geschlecht <- replace(cps.neu$Geschlecht, list = cps.neu$Geschlecht==2, values = 0)
```

*** =sct
```{r}
test_or({
  test_function("replace", args = c("list","values"), not_called_msg = "Lösen Sie diese Aufgabe bitte mit der Funktion `replace`.", incorrect_msg = "Der Funktionsaufruf ist so nicht korrekt. Überprüfen Sie bitte ihre Eingaben.")
},{ 
  fun <- ex() %>% override_solution("cps.neu$Geschlecht <- replace(cps.neu$Geschlecht, list = which(cps.neu$Geschlecht==2), values = 0)") %>% check_function("replace")
  fun %>% check_arg("list") %>% check_equal()
  fun %>% check_arg("values") %>% check_equal()
},{
  fun <- ex() %>% override_solution("cps.neu$Geschlecht <- replace(cps.neu$Geschlecht, list = cps$a_sex==2, values = 0)") %>% check_function("replace")
  fun %>% check_arg("list") %>% check_equal()
  fun %>% check_arg("values") %>% check_equal()
})

test_object("cps.neu", eq_condition = "equal", incorrect_msg = "Das Objekt `cps.neu` ist falsch definiert.")
success_msg("Weiter so!")
```

--- type:NormalExercise lang:r xp:100 skills: key:6079bb2eb5
## B1 Ein Dummy-Regressionsmodell für den Stundenlohn 

Sie vermuten die folgende Beziehung zwischen Studenlohn und Geschlecht:
  
  $$ Stundenlohn = \beta\_0 + \beta\_1 \times Geschlecht + u $$
  
  *Der Datensatz `cps.neu` aus der vorherigen Aufgabe ist in Ihrer Arbeitsumgebung verfügbar.*
  
*** =pre_exercise_code
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
cps.neu <- cps
names(cps.neu) <- c("Geschlecht","Jahr","Stundenlohn")
cps.neu$Geschlecht <- replace(cps.neu$Geschlecht, cps.neu$Geschlecht==2, 0)
```

*** =instructions 
- Schätzen Sie das oben genannte Modell mit der KQ-Methode und speichern Sie das Ergebnis in `mod`.


*** =hint

Schätzen Sie das Modell mit der Funktion `lm`. Für weitere Hinweise benutzen Sie bitte die Hilfefunktion: `?lm`.

*** =sample_code
```{r}
# Schätzen Sie das Modell und erstellen Sie `mod`.



```

*** =solution
```{r}
# Schätzen Sie das Modell und erstellen Sie `mod`.
mod <- lm(Stundenlohn ~ Geschlecht, data = cps.neu)
```

*** =sct
```{r}
test_predefined_objects("cps.neu")

test_or({
  fun <- ex() %>% check_function('lm')
  fun %>% check_arg('formula') %>% check_equal("Das Argument Formula ist falsch definiert.")
  fun %>% check_arg('data') %>% check_equal()
},{
  fun <- ex() %>% override_solution('attach(cps.neu); mod <- lm(Stundenlohn ~ Geschlecht)') 
  fun %>% check_function('lm')  %>% check_arg('formula') %>% check_equal()
},{
  ex() %>% override_solution('mod <- lm(cps.neu$Stundenlohn ~ cps.neu$Geschlecht)') %>% check_function('lm') %>% check_arg('formula') %>% check_equal()
})

success_msg("Weiter so!")
```

--- type:NormalExercise lang:r xp:100 skills: key:c77c0e6270
## B2 Das Modellobjekt

*Der Datensatz `cps.neu` und das Modell `mod` aus der vorherigen Aufgabe sind in Ihrer Arbeitsumgebung verfügbar.*
  
*** =pre_exercise_code
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
cps.neu <- cps
names(cps.neu) <- c("Geschlecht","Jahr","Stundenlohn")
cps.neu$Geschlecht <- replace(cps.neu$Geschlecht, cps.neu$Geschlecht==2, 0)
mod <- lm(Stundenlohn ~ Geschlecht, data = cps.neu)
```

*** =instructions
- Verschaffen Sie sich einen Überblick über das in der letzten Aufgabe geschätzte Modell `mod`. 
- Vergewissern Sie sich, dass `mod` ein Objekt vom Typ `list` ist.

*** =hint

Einen Überblick über ein Objekt erhalten Sie mit `summary`. `is.list` prüft auf den Typ `list`.

*** =sample_code
```{r}
# Verschaffen Sie sich einen Überblick des Regressionsergebnisses


# Zeigen Sie, dass `mod` vom Typ `list` ist.


```

*** =solution
```{r}
# Verschaffen Sie sich einen Überblick über das Modell.
summary(mod)

# Zeigen Sie, dass `mod` vom Typ `list` ist.
is.list(mod)
```

*** =sct

```{r}
test_or({
  test_function("summary", args="object")
},{
  ex() %>% override_solution("summary(lm(cps.neu$Stundenlohn ~ cps.neu$Geschlecht))") %>% check_function('summary') %>% check_arg('object') %>% check_equal()
}, incorrect_msg="Etwas ist falsch gelaufen.")

test_or({
  test_function("is.list")
},{
  ex() %>% override_solution('typeof(mod)') %>% check_function('typeof')
})

success_msg("Weiter so!")
```

--- type:NormalExercise lang:r xp:150 skills: key:987ca6ad29
## B3 Koeffizienten und Konfidenzintervalle

*Der Datensatz `cps.neu` und das Modell `mod` aus der vorherigen Aufgabe sind in Ihrer Arbeitsumgebung verfügbar!*
  
*** =pre_exercise_code
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
cps.neu <- cps
names(cps.neu) <- c("Geschlecht","Jahr","Stundenlohn")
cps.neu$Geschlecht <- replace(cps.neu$Geschlecht, cps.neu$Geschlecht==2, 0)
mod <- lm(Stundenlohn ~ Geschlecht, data = cps.neu)
```

*** =instructions
- `mod` enthält den Eintrag `coefficients`, eine Matrix mit geschätzten Koeffizienten. Greifen Sie diese Matrix ab und speichern Sie das Ergebnis in `coef`.
- Nutzen Sie die Funktion `confint` um 95%-Konfidenzintervalle für die Koeffizienten im Modell `mod` zu schätzen.

*** =hint

- Objekte in benannten Listen können mit `$` referenziert werden. Welches Objekt in der Liste `mod` ist für Sie von Interesse? Lesen Sie dieses aus und speichern Sie es in `coef` mittels `<-`.
- Die Funktion `confint` berechnet standardmäßig 95%-Konfidenzintervalle für geschätzte Koeffizienten.


*** =sample_code
```{r}
# Erstellen Sie das Objekt `coef`.


# Berechnen Sie die Konfidenzintervalle.

```

*** =solution
```{r}
# Erstellen Sie das Objekt `coef`.
coef <- mod$coefficients

# Berechnen Sie die Konfidenzintervalle.
confint(mod)
```

*** =sct
```{r}
test_predefined_objects("mod")
test_or({
  test_student_typed("mod$coefficients")
},{
  test_student_typed("mod$coef")
},{
  ex() %>% override_solution('coef <- coefficients(mod)') %>% check_function('coefficients')
},{
  test_student_typed("mod[[1]]")
})


test_object("coef")


test_function("confint")


success_msg("Weiter so!")
```

--- type:NormalExercise lang:r xp:100 skills: key:d63791df76
## B4 Interpretation

Betrachten Sie nun das zuvor geschätzte Regressionsmodel:
  
  $$ \widehat{Stundenlohn} = \underset{(0.1135)}{21.72599} + \underset{(0.1577)}{4.00675} \times Geschlecht $$
  
  Das Plot-Panel zeigt Ihnen eine graphische Darstellung dieses Resultats.

Erinnern Sie sich: $Geschlecht$ ist eine Binäre Variable.

$$ Geschlecht = \begin{cases} 0 & \text{wenn weiblich,} \\\\ 1 & \text{sonst.}  \end{cases} $$
  
  *Der Datensatz `cps.neu`, das Regressionsobjekt `mod` sowie die Matrix `coef` aus der letzten Aufgabe sind Ihrer der Arbeitsumgebung verfügbar!*
  
*** =pre_exercise_code
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";", dec = ".")
cps.neu <- cps
names(cps.neu) <- c("Geschlecht","Jahr","Stundenlohn")
cps.neu$Geschlecht <- replace(cps.neu$Geschlecht, cps.neu$Geschlecht==2, 0)
mod <- lm(Stundenlohn ~ Geschlecht, data = cps.neu)
plot(Stundenlohn ~ Geschlecht, data=cps.neu[sample(1:nrow(cps.neu), size = 1000),],pch=20, cex=0.6, col="steelblue", xaxt="n")
axis(1, at =c(0,1))
points(c(0,1),c(mod$coef[1],sum(mod$coef)), col = "red", pch=20, cex=1)
coef <- mod$coefficients
```


*** =instructions

- Wie hoch sind die geschätzten Studenlöhne für Männer und Frauen? *Runden Sie ihre Ergebnisse auf 2 Nachkommastellen* und weisen Sie die Werte den Variablen `dLohn.Mann` und `dLohn.Frau` zu!
  
  
*** =hint

- Sie können der Modellgleichung die zur Berechnung nötigen Werte entnehmen. 
- Runden können Sie mit der Funktion `round`. Diese Funktion besitzt ein Argument, mit dem Sie die Anzahl der Nachkommastellen festlegen können.

*** =sample_code
```{r}
# Geben Sie die geschätzten Stundenlöhne für Männer und Frauen an.


```

*** =solution
```{r}
# Geben Sie die geschätzten Stundenlöhne für Männer und Frauen an.
dLohn.Frau <- round(21.72599,2)
dLohn.Mann <- round(21.72599 + 4.00675,2)
```

*** =sct
```{r}
test_predefined_objects("mod")

test_object("dLohn.Frau")

test_or({
  test_object("dLohn.Mann")
},{
  ex() %>% override_solution("dLohn.Mann <- round(21.72599,2) + round(4.00675,2)") %>% check_object("dLohn.Mann") 
})
```

--- type:NormalExercise lang:r xp:200 skills: key:4bffa84edc
## B5 Modellgüte

*Der Datensatz `cps.neu` und das Regressionsobjekt `mod` aus der letzten Aufgabe sind in Ihrer Arbeitsumgebung verfügbar!*
  
*** =pre_exercise_code
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";", dec = ".")
cps.neu <- cps
names(cps.neu) <- c("Geschlecht","Jahr","Stundenlohn")
cps.neu$Geschlecht <- replace(cps.neu$Geschlecht, cps.neu$Geschlecht==2, 0)
mod <- lm(Stundenlohn ~ Geschlecht, data = cps.neu)
```

*** =instructions
- Speichern Sie die Residuen des Modells in den Vektor `res`.
- Bestimmen Sie $SSR$ für das Model. Speichern Sie das Ergebnis als `SSR`.
- Berechnen Sie $TSS$ für das Model. Speichern Sie das Ergebnis als `TSS`.
- Nutzen Sie Ihre Ergebnisse, um $R^2$ zu berechnen. Speichern Sie den Wert in `R2`.


*** =hint
- Nutzen Sie die Funktion `residuals`.
- Es gilt $SSR = \sum_{i=1}^n \hat{u}^2\_i$ und $TSS = \sum\_{i=1}^n (y\_i - \overline{y})^2$ sowie $R^2 = 1 - SSR/TSS$. 
- Sie können den Rechenaufwand verringern, indem Sie geschickt auf zur Verfügung stehende Objekte zurückgreifen! Denken Sie bspw. an `summary`.

*** =sample_code
```{r}
# Berechnen Sie die genannten Größen.




```

*** =solution
```{r}
# Berechnen Sie die genannten Größen.
res <- residuals(mod)
SSR <- sum(res^2)
TSS <- sum((cps.neu$Stundenlohn-mean(cps.neu$Stundenlohn))^2)
R2 <- 1- SSR/TSS
```

*** =sct
```{r}
test_predefined_objects(c("mod","cps.neu"))
test_object("res")
test_object("SSR")
test_object("TSS")
test_object("R2")
success_msg("Weiter so!")
```

--- type:NormalExercise lang:r xp:150 skills: key:4a9f66f0d7
## B6 Inferenz

Betrachten Sie erneut das geschätzte Regressionsmodell:
  
  $$ \widehat{Stundenlohn} = \underset{(0.1135)}{21.72599} + \underset{(0.1577)}{4.00675} \times Geschlecht $$
  
  *Der Datensatz `cps.neu` und das Regressionsobjekt `mod` aus der letzten Aufgabe sind Ihrer der Arbeitsumgebung verfügbar!*
  
*** =pre_exercise_code
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";", dec = ".")
cps.neu <- cps
names(cps.neu) <- c("Geschlecht","Jahr","Stundenlohn")
cps.neu$Geschlecht <- replace(cps.neu$Geschlecht, cps.neu$Geschlecht==2, 0)
mod <- lm(Stundenlohn ~ Geschlecht, data = cps.neu)
```

*** =instructions
- Berechnen Sie $t$-Statistiken für die individuellen Tests der Hypothesen $H\_{0,\beta\_0}: \beta\_0 = 0$ und $H\_{0,\beta\_1}: \beta\_1 = 0$. Runden Sie auf 2 Nachkommastellen. Speichern Sie die Resultate in `t.a` und `t.b`!
  
*** =hint
- Die allgemeine Formel der $t$-Statistik eines Regressionskoeffizienten lautet $\frac{\hat{\beta}\_i-\beta\_{i,0}}{\widehat{s.d.}(\hat{\beta}\_i)}$.
- Geschätzte Standardfehler stehen in Klammern under dem jeweiligen geschätzten Koeffizienten.
- Sie können den Rechenaufwand verringern, indem Sie geschickt auf zur Verfügung stehende Objekte zurückgreifen! Denken Sie bspw. an `summary`.

*** =sample_code
```{r}
# Berechnen Sie die t-Statistiken.


```

*** =solution
```{r}
# Berechnen Sie die t-Statistiken.
t.a <- round(summary(mod)$coefficients[1,3],2)
t.b <- round(summary(mod)$coefficients[2,3],2)
```

*** =sct
```{r}
test_predefined_objects("mod")
test_or({
  test_object("t.a")
  test_object("t.b")
},{
  ex() %>% override_solution("t.a <- round(21.72599/0.1135,2);t.b <- round(4.00675/0.1577,2)") %>% check_object(c("t.a","t.b"))
})

success_msg("Weiter so!")
```

