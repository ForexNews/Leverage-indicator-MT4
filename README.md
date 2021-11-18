# Leverage-indicator-MT4
![Leverage Indicator MT4 Screen](https://forexnew.org/wp-content/uploads/2021/09/Leverage-Indicator.png)
- Leverage indicator is a tool for checking the current leverage of a trading account.
- Useful to monitor, if broker changing leverage, during the economic news announcements.
- Real-time leverage monitoring.
- Coding for MetaTrader 4 platform and all brokers.
- See working example at [Leverage indicator](https://forexnew.org/คลังความรู้/leverage-คืออะไร/#indicators)

## Inputs Parameter
![Leverage Indicator MT4 Input](https://forexnew.org/Download/Leverage-indicator-input.png)
- Text Size : 9
- Text Color : MintCream
- Panel Color : SteelBlue
- Panel Width : 155
- Panel Height : 35
- Position X : 20
- Position Y : 25

### MQL4 Code

```
#property copyright    "ForexNew.org Opensource"
#property link         "https://forexnew.org/"
#property version      "1.0"
#property description  "- Leverage Indicator"
#property description  "- Indicator for Metatrader 4"
#property strict
#property indicator_chart_window

extern int Text_Size=9;  // Text Size
extern color Text_Color=MintCream;  // Text Color
extern color Panel_Color=SteelBlue;  // Panel Color
string Font_Setting="Arial Black";
extern int Panel_Width=150;  // Panel Width
extern int Panel_Height=35;  // Panel Height
extern int Position_X=20; // Position X
extern int Position_Y=25; // Position Y
int positionsetx=Position_X+12;
int positionsety=Position_Y+10;

int init()
{
   Check_Leverage();
   return(INIT_SUCCEEDED);
}

int start()
{
   Check_Leverage();
   return(INIT_SUCCEEDED);
}

void Check_Leverage()
{
   int leverage = AccountLeverage();
   
// Create panel and text Label on the screen //
   ObjectCreate("Main_Panel",OBJ_RECTANGLE_LABEL,0,0,0,0,0,0);
   ObjectSet("Main_Panel",OBJPROP_BGCOLOR,Panel_Color);
   ObjectSet("Main_Panel",OBJPROP_CORNER,0);
   ObjectSet("Main_Panel",OBJPROP_BACK,true);
   ObjectSet("Main_Panel",OBJPROP_XDISTANCE,Position_X);
   ObjectSet("Main_Panel",OBJPROP_YDISTANCE,Position_Y);
   ObjectSet("Main_Panel",OBJPROP_XSIZE,Panel_Width);
   ObjectSet("Main_Panel",OBJPROP_YSIZE,Panel_Height);
   ObjectSet("Main_Panel", OBJPROP_SELECTABLE, false);
   ObjectSet("Main_Panel", OBJPROP_HIDDEN, true);
   
   ObjectCreate("Leverage_Label", OBJ_LABEL, 0, 0, 0);
   ObjectSet("Leverage_Label", OBJPROP_CORNER, 0);
   ObjectSet("Leverage_Label", OBJPROP_XDISTANCE, positionsetx);
   ObjectSet("Leverage_Label", OBJPROP_YDISTANCE, positionsety);
   ObjectSetText("Leverage_Label", "Leverage = 1:"+leverage, Text_Size, Font_Setting, Text_Color);
   ObjectSet("Leverage_Label", OBJPROP_SELECTABLE, false);
   ObjectSet("Leverage_Label", OBJPROP_HIDDEN, true);
   
   ObjectCreate("Custom_Label", OBJ_LABEL, 0, 0, 0);
   ObjectSetText("Custom_Label","Copyright: ForexNew.org - Free Opensource",9, "Arial", DeepSkyBlue);
   ObjectSet("Custom_Label", OBJPROP_CORNER, 2);
   ObjectSet("Custom_Label", OBJPROP_XDISTANCE, 10);
   ObjectSet("Custom_Label", OBJPROP_YDISTANCE, 10);
   ObjectSet("Custom_Label", OBJPROP_SELECTABLE, false);
   ObjectSet("Custom_Label", OBJPROP_HIDDEN, true);
   WindowRedraw();
}

// Delete panel and text label when removing the indicator //
void OnDeinit(const int reason)
{
   ObjectsDeleteAll(0,"Main_Panel");
   ObjectsDeleteAll(0,"Leverage_Label");
   ObjectsDeleteAll(0,"Custom_Label");
}
```
#### Visit our website
- [ForexNew.org](https://forexnew.org/)
