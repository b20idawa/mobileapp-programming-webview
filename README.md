
# Rapport

Enable internetaccess:
För att applikationen ska få tillgång till internet har kod lagts till i xml-filen ”AndroidManifest”. I koden anges ”uses-permission” som möjliggör att olika tillåtelser kan implementeras i applikationen. Med hjälp av ”android.permission.INTERNET” tillåts internetåtkomst i applikation vilket möjliggör att externa webbsidor kan visas för användaren. Den rad kod som innehåller tillåtelsen är placerad ovanför ”application” i XML-filen.

```
 <uses-permission android:name="android.permission.INTERNET" />
```

Create a webview element:
För att skapa ett webview element för applikationen har kod både lagts till och tagits bort i xml-filen ”content_main”. För att implementera ett webview element har det befintliga textview elementet tagits bort i koden. Genom att ta bort textview elementet visas inte längre ”hello world” på applikationens startsida. Den kod som adderats i xml-filen innehåller tre rader kod som tillsammans skapar ett webview element till applikationen. Dessutom har det id som är applicerat på elementet ändrats till ”my_webview” istället för enbart webview som det var tidigare. Sist har också margintop lagts till för att webbidorna som visas inte ska hamna bakom appens topbar.

```
    <WebView
        android:id="@+id/my_webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_marginTop="55dp" />
```

Create a private member:
I filen ”mainactivity” har en “private member” skapats genom att ange private tillsammans med ett element som i detta fall är webview. På samma rad kod anges också mywebview som namn på den ”private member” som skapats. Den privata medlemmen deklareras därefter till det id som angetts på webview elementet med hjälp av ”findviewbyid”. Med hjälp av ”findviewbyid” anropas elementets ID och kan därefter appliceras på den ”private member” som skapats.

```
    private WebView mywebview;
```
```
    mywebview = findViewById(R.id.my_webview);
```

Enable Javascript:
För att applikationen ska kunna visa externa webbsidor som använder Javascript måste Javascript aktiveras. Javascript är i ursprungsläget inte aktiverat i webview läget och måste därför aktiveras för att kunna användas. För att aktivera programspråket har två rader kod lagts till i ”mainactivity-filen”. Koden som lagts till styr websettings för applikationen och anger att tillåtelsen för Javascript ska vara ”true” och inte ”false” som i grundinställningarna.

```
    WebSettings webSettings = mywebview.getSettings();
    webSettings.setJavaScriptEnabled(true);
```

Add HTML page as an asset:
För att skapa en asset-folder har en ny mapp skapats i den redan befintliga app-mappen. Inuti den asset-folder som skapats har en ny ”directory” utformats som är en undermapp till tillgångsmappen. Undermappen innehåller sedan en html-fil som vid detta laget är tom på innehåll. För att anropa på html-filen i ”mainactivity” har ”mywebview.loadUrl” använts. Den url som ska hämtas är inte en länk från en webbsida utan är en filåtkomst. Inom parentesen anges därför först den mapp som filen ligger i och därefter filens namn som i detta fall är webview.html.

```
    mywebview.loadUrl("file:///android_asset/webview.html");
```

Instantiate mywebview in "onCreate()":
För att starta "private member" i "onCreate()" anges tre rader kod. Den första raden kod kallar på webview-elementet genom att anropa det id som angetts. De två nästkommande rader kod skapar en webviewclient som kommer att användas för att presentera en webbsida i applikationen. Utan en webclient kommer webbsidor öppnas i en webbläsare istället för direkt i applikationen vilket inte är målet. Därför skapas en webclient för applikationen som kommer att användas för att öppna webbsidor.

```
    mywebview = findViewById(R.id.my_webview);
    WebViewClient myWebViewClient = new WebViewClient();
    mywebview.setWebViewClient(myWebViewClient);
```

Implement and call showexternalwebpage and showinternalwebpage:
I ”mainactivity” finns två stycken ”public void” som från början är tomma på innehåll. Funktionerna ska fyllas med kod som styr vilket innehåll som ska visas på respektive sida i applikationen. Den första funktionen heter ”showexternalwebpage” och den andra heter ”showinternalwebpage”. Innehållet i funktionerna liknar varandra men skiljer sig på den länk som anges. Båda funktionerna börjar med att ange mywebview som är en "private member" tilsammans med loadUrl följt av en parentes. Inom parentesen anges en länk till antingen en extern webbsida eller en intern fil. I funktionen för externalwebpage används en http-länk som är hämtad från internet. Den externa websidan som kommer att visas är his.se. I funktionen internalwebpage används istället en file-länk som anger en fil i projektet som ska visas på sidan i applikationen. Den interna sidan som kommer att visas är en html-fil som innehåller en rubrik med tillhörande styling.

```
    public void showExternalWebPage(){
            mywebview.loadUrl("https://his.se");
        }
```
```
     public void showInternalWebPage(){
            mywebview.loadUrl("file:///android_asset/webview.html");
        }
```

För att anropa på funktionerna via den rullgardinsmeny som finns i applikationen har kod adderats till en loop i ”mainactivity”. Inuti loopen finns två stycken if-satser som styr respektive menyval i rullgardinsmenyn. Den första if-satsen styr vilket innehåll som ska visas när användaren trycker på externalwebpage. På den externa webbsidan ska his.se visas och därför anropas funktionen ”showexternalwebpage” inom den första if-satsen. Den andra if-satsen styr vilket innehåll som ska visas när användaren trycker på internalwebpage. På den interna sidan ska html-filen visas och därför anropas funktionen ”showinternalwebpage” inom den andra if-satsen.

```
    if (id == R.id.action_external_web) {
           Log.d("==>","Will display external web page");
           showExternalWebPage();
           return true;
    }
```
```
     if (id == R.id.action_internal_web) {
            Log.d("==>","Will display internal web page");
            showInternalWebPage();
            return true;
     }
```

Screenshot externlwebpage:
![](screenshot_externalwebpage.png)

Screenshot internalwebpage:
![](screenshot_internalwebpage)