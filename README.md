# FER-2013 Emotion Classification

Det här projektet är en individuell inlämningsuppgift i Deep Learning. Målet är att bygga, träna och utvärdera en CNN-modell som kan klassificera ansiktsuttryck från bilder.

Datasetet som används är **FER-2013**, som består av gråskalebilder av ansikten i storleken 48x48 pixlar. Bilderna är uppdelade i träningsdata och testdata, där varje ansiktsuttryck ligger i en egen mapp.

## Klasser i datasetet

Modellen tränas på sju olika ansiktsuttryck:

- angry
- disgust
- fear
- happy
- neutral
- sad
- surprise

## Projektets innehåll

Projektet innehåller:

- dataförståelse och klassfördelning
- förberedelse av bilddata
- normalisering av pixelvärden
- träning av CNN-modeller
- jämförelse mellan två modellvarianter
- utvärdering med accuracy, classification report och confusion matrix
- prediktion på en bild från testdatan
- analys av overfitting, generalisering och modellens begränsningar
- sparad modell i `.keras`-format

## Modellvarianter

I notebooken testas två modeller.

### Modell 1: Baseline CNN

Modell 1 är en enklare CNN-modell som används som första fungerande modell och jämförelsepunkt. Den består av convolutional layers, max pooling och dense layers.

### Modell 2: Förbättrad CNN

Modell 2 är en mer utvecklad CNN-modell med:

- fler convolutional layers
- batch normalization
- dropout
- data augmentation
- callbacks som EarlyStopping och ReduceLROnPlateau

Syftet med modell 2 var att testa om en mer utvecklad modell kunde generalisera bättre än baseline-modellen.

## Resultat

Modell 1 fick cirka **41,93 % test accuracy**.

Modell 2 fick cirka **50,03 % test accuracy**.

Resultatet visar att modell 2 presterade bättre på testdatan än modell 1. Modell 1 hade högre training accuracy än modell 2, men lägre validation accuracy och test accuracy. Det tyder på att modell 1 hade mer problem med overfitting.

Modell 2 hade mer jämna resultat mellan träning, validering och testdata. Det tyder på att dropout, batch normalization och data augmentation hjälpte modellen att generalisera bättre.

Modellen fungerade bäst på klassen `happy`, medan `disgust` var svårast. Det beror troligen på att `disgust` har mycket färre bilder än de andra klasserna i datasetet.

## Projektstruktur

```text
fer2013-emotion-classification/
├── data/
│   └── raw/
│       └── FER-2013/
├── images/
├── models/
│   └── model_2_improved_cnn.keras
├── notebooks/
│   └── fer2013_emotion_classification.ipynb
├── .gitignore
├── README.md
└── requirements.txt
```

Datasetet ligger lokalt i `data/raw/`, men pushas inte till GitHub eftersom det är stort. Projektet är därför uppbyggt så att datasetet läggs till lokalt innan notebooken körs.

## Installation

Installera projektets dependencies med:

```bash
pip install -r requirements.txt
```

## Köra projektet

Öppna notebooken:

```text
notebooks/fer2013_emotion_classification.ipynb
```

Kör cellerna uppifrån och ner.

Notebooken innehåller både kod och rapportdelar i markdown.

## Dataset

Datasetet FER-2013 behöver ligga i följande struktur lokalt:

```text
data/raw/FER-2013/
├── train/
│   ├── angry/
│   ├── disgust/
│   ├── fear/
│   ├── happy/
│   ├── neutral/
│   ├── sad/
│   └── surprise/
└── test/
    ├── angry/
    ├── disgust/
    ├── fear/
    ├── happy/
    ├── neutral/
    ├── sad/
    └── surprise/
```

## Sparad modell

Den bästa modellen sparas i mappen `models/` som en `.keras`-fil:

```text
models/model_2_improved_cnn.keras
```


## Reflektion

Projektet visar att det inte räcker att bara bygga en modell och titta på training accuracy. Det är viktigt att också jämföra med validation och testdata för att förstå om modellen faktiskt generaliserar.

En viktig lärdom från projektet är att en mer avancerad modell inte automatiskt betyder att training accuracy blir högst. I detta fall fick modell 2 lägre training accuracy än modell 1, men bättre testresultat och mer stabil generalisering.

Det visar att generalisering är viktigare än att modellen bara presterar bra på träningsdatan.