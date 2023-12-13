<p><a href="https://www.skia4delphi.org"><img src="../Assets/Artwork/logo-gradient.svg" alt="Logo" height="300" width="360" /></a></p>

#  Label

## TSkLabel

**TSkLabel** is the control that implements the SkParagraph internally, having several more features than the TLabel, such as:

 - Font families; (font fallback list like in css)
 - Font weight;
 - Font slant;
 - Support for multiple styles in text;
 - Support for BiDi; (Right-to-Left)
 - Support justify horizontal alignment;
 - Support custom font; (without install the font)
 - Limit the maximum number of lines;
 - Auto size option; (width and height)
 - Advanced decorations; (like underline wavy, overline, dashed line, among others...)
   **and much more...**

![Label](https://user-images.githubusercontent.com/16469061/153615162-e2f51dd6-b22e-4f34-9493-244122faa5ae.png#gh-light-mode-only)
![Label](https://user-images.githubusercontent.com/16469061/153615217-53e851a3-c20d-4cb9-92fb-b9b18319c342.png#gh-dark-mode-only)

### Firemonkey styles

In Firemonkey, the TSkLabel supports FMX styles too. It is very recommended, because with that, you'll be able to automatically change the properties of your label, and create, for example, themes light and dark for your application, as in FMX's TLabel. To use styles in TSkLabel, follow the steps:

1. Open the Style Designer form (double click in the TStyleBook of your form)
2. Add the follow style object by copying the code below and pasting it into the StyleContainer (in the Style Designer form)
   ```pascal
   object TLayout
     StyleName = 'SkLabel1Style1'
     Align = Center
     Size.Width = 0.000000000000000000
     Size.Height = 0.000000000000000000
     Size.PlatformDefault = False
     object TSkStyleTextObject
      StyleName = 'text'
     end
   end
   ```
3. Edit the text object (TSkStyleTextObject) any way you want, like setting color to Red
4. Close the Style Designer form, will show a prompt asking to Apply, press Yes
5. Now, the style for TSkLabel that you created, will be available to select in TSkLabel.StyleLookup property

*Note: The style with the name "sklabelstyle" is always the default style of the TSkLabel.StyleLookup, even when it is empty.*

# Right-to-left

The right-to-left is made automatically after change the BiDi property of the form to RightToLeft.

# Custom fonts

It is possible to use custom font in the TSkLabel in a very simple way. Just register them in the app initialization:

## FMX

```pascal
program Project1;

uses
  System.StartUpCopy,
  FMX.Forms,
  FMX.Skia,
  Unit1 in 'Unit1.pas' {Form1};

{$R *.res}

begin
  TSkDefaultProviders.RegisterTypeface('Poppins.ttf');
  Application.Initialize;
  Application.CreateForm(TForm1, Form1);
  Application.Run;
end.
```

On RAD Studio 12 Athens or newer it is recommended to use `IFMXFontManagerService`:

```pascal
program Project1;

uses
  System.StartUpCopy,
  FMX.Forms,
  FMX.Platform,
  FMX.FontManager,
  Unit1 in 'Unit1.pas' {Form1};

{$R *.res}

begin
  var LFontManager: IFMXFontManagerService;
  if TPlatformServices.Current.SupportsPlatformService(IFMXFontManagerService, LFontManager) then
    LFontManager.AddCustomFontFromFile('Poppins.ttf');
  Application.Initialize;
  Application.CreateForm(TForm1, Form1);
  Application.Run;
end.
```

## VCL

```pascal
program Project1;

uses
  Vcl.Forms,
  Vcl.Skia,
  Unit1 in 'Unit1.pas' {Form1};

{$R *.res}

begin
  TSkDefaultProviders.RegisterTypeface('Poppins.ttf');
  Application.Initialize;
  Application.MainFormOnTaskbar := True;
  Application.CreateForm(TForm1, Form1);
  Application.Run;
end.
```
