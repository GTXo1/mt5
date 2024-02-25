#include <Canvas\Canvas.mqh>
#property  copyright "Valeriia Mishchenko"
#property version    "2.12"
#property strict
#property description  "Waka Waka EA"

  enum LotSizingEnum      {LowRiskPreset = 5,//Low Risk Set 20% annual (0.25% load)
                   MidRiskPreset = 4,//Mid Risk Set 40% annual (0.5% load)
                   HighRiskPreset = 3,//Significant Risk Set 80% annual (1.0% load)
                   ExtremeRiskPreset = 7,//High Risk Set 120% annual (1.5% load)
                   LotsEquity = 2,//Dynamic Lot based on Equity
                   LotsBalance = 1,//Dynamic Lot based on Balance
                   LotsDepositLoad = 6,//Lots based on Deposit load
                   FixedLots = 0//Fixed Lot
                     };
  enum AllowBuySellEnum      {AllowSell2 = 2,//Sell only
                   AllowBuy1 = 1,//Buy only
                   AllowBuySell0 = 0//Buy and Sell
                     };
  enum eMaxDrawdownAction      {IgnoreNewUntilRestart = 3,//Prohibit opening new grids until restart
                   IgnoreNewSignals = 2,//Prohibit opening new grids
                   CloseStopTradingUntilRestart = 1,//Close trades & stop trading until restart
                   CloseStopTradingFor24h = 0//Close trades & stop trading for 24h
                     };
  enum eDrawdownCalculation      {ThisStrategy = 1,//This strategy
                   TheAccount = 0//The account
                     };


//------------------
class CCanvasX : public CCanvas  { public:
              //    CCanvasX(void);
                bool CCanvasX_12( string uuu_0_st);
         };
   //  CCanvasX::CCanvasX(void){m_style=0xFFFFFFFF;m_style_idx=0;m_chart_id=0;m_objname=NULL;m_objtype=-1;m_rcname=NULL;m_width=0;m_height=0;m_format=0;m_fontname="arial";m_fontsize=-120;m_fontflags=0;m_fontangle=0;};
class SymbolInformation  { public:string  st_1; datetime  da_2; datetime  da_3; int  in_4; bool  bo_5; bool  bo_6; datetime  da_7; datetime  da_8; double  do_9; bool  bo_10; bool  bo_11; double  do_12; double  do_13; int  in_14; int  in_15; long  lo_16; double  do_17; bool  bo_18; bool  bo_19; bool  bo_20; int  in_21; double  do_22; double  do_23; double  do_24; double  do_25; double  do_26; datetime  da_27; datetime  da_28; 
                void SymbolInformation_13();
                void SymbolInformation_14();
                void SymbolInformation_15();
                void ~SymbolInformation();
         };
class CutTrade  { public:long  lo_1; double  do_2; bool  bo_3; 
                void CutTrade_17();
                void CutTrade_18();
                void CutTrade_19();
                void ~CutTrade();
         };
input string __MM_Setting__="Select the risk settings"  ;   //------> MM & Risk settings <------
string MM_Setting = __MM_Setting__;
input bool __AllowOpeningNewGrid__=true  ;    //Allow Opening a new Grid?
bool AllowOpeningNewGrid = __AllowOpeningNewGrid__;
input LotSizingEnum __LotSizingMethod__=5  ;    //Lot-sizing Method
LotSizingEnum LotSizingMethod = __LotSizingMethod__;
input double __LotSizingValueFixed__=0.01  ;    //Fixed Lot
double LotSizingValueFixed = __LotSizingValueFixed__;
input double __LotSizingValueDynamic__=10000  ;    //Dynamic Lot (Balance/Equity based)
double LotSizingValueDynamic = __LotSizingValueDynamic__;
input double __LotSizingDepositLoadPercent__=0.25  ;    //Deposit Load %
double LotSizingDepositLoadPercent = __LotSizingDepositLoadPercent__;
input bool __FixedInitialDeposit__=false ;    //Fixed Initial Deposit? (Tester only)
bool FixedInitialDeposit = __FixedInitialDeposit__;
input double __MaximumLot__=100  ;    //Maximum Lot
double MaximumLot = __MaximumLot__;
input bool __AutoSplit__=false ;    //Auto Split?
bool AutoSplit = __AutoSplit__;
input double __MaximumSpread__=10  ;    //Maximum Spread, in pips
double MaximumSpread = __MaximumSpread__;
input double __MaximumSlippage__=10  ;    //Maximum Slippage for a non-ECN acc, in pips
double MaximumSlippage = __MaximumSlippage__;
input int __MaximumSymbols__=2  ;    //Maximum Symbols at a time
int MaximumSymbols = __MaximumSymbols__;
input bool __AllowHedging__=true  ;    //Allow Hedging?
bool AllowHedging = __AllowHedging__;
input bool __AllowTradingOnHolidays__=false ;    //Allow Trading on Holidays?
bool AllowTradingOnHolidays = __AllowTradingOnHolidays__;
input AllowBuySellEnum __AllowToBuySell__=0  ;    //Allow to Buy/Sell
AllowBuySellEnum AllowToBuySell = __AllowToBuySell__;
input double __MinimumFreeMargin__=0  ;    //Minimum Free Margin % [0-disabled]
double MinimumFreeMargin = __MinimumFreeMargin__;
input double __MaximumDrawdown__=100  ;    //Max Floating Drawdown %
double MaximumDrawdown = __MaximumDrawdown__;
input double __MaximumDrawdownMoney__=0  ;    //Max Floating Drawdown in Money [0-disabled]
double MaximumDrawdownMoney = __MaximumDrawdownMoney__;
input eMaxDrawdownAction __MaximumDrawdownAction__=0  ;    //Max Drawdown Action
eMaxDrawdownAction MaximumDrawdownAction = __MaximumDrawdownAction__;
input eDrawdownCalculation __DrawdownCalculation__=1  ;    //Max Drawdown Calculation
eDrawdownCalculation DrawdownCalculation = __DrawdownCalculation__;
input string __Strategy_Setting__="Select the strategy settings and symbols used"  ;   //------> Strategy settings <------
string Strategy_Setting = __Strategy_Setting__;
input string __Symbols__="AUDNZD,AUDCAD,NZDCAD"  ;   //Symbols separated by comma (custom if empty)
string Symbols = __Symbols__;
input int __HourToStartTrading__=0  ;    //Hour to Start Trading (broker\'s time)
int HourToStartTrading = __HourToStartTrading__;
input int __HourToStopTrading__=23  ;    //Hour to Stop Trading (broker\'s time)
int HourToStopTrading = __HourToStopTrading__;
input int __BollingerBandsPeriod__=35  ;    //Bollinger Bands Period
int BollingerBandsPeriod = __BollingerBandsPeriod__;
input int __RSI_Period__=20  ;    //RSI Period
int RSI_Period = __RSI_Period__;
input int __RSI_Value__=15  ;    //Maximum RSI Value
int RSI_Value = __RSI_Value__;
input string __Strategy_Setting_TP__="Select TP settings"  ;   //------> TakeProfit settings <------
string Strategy_Setting_TP = __Strategy_Setting_TP__;
input double __InitialTP__=10  ;    //TakeProfit for Initial Trade, in pips
double InitialTP = __InitialTP__;
input bool __WeightedTP__=true  ;    //Weighted TakeProfit?
bool WeightedTP = __WeightedTP__;
input double __GridTP__=0  ;    //TakeProfit for Grid, in pips (can also be zero or negative)
double GridTP = __GridTP__;
input int __BreakEvenAfterThisLevel__=0  ;    //Break Even after this Level [0-disabled]
int BreakEvenAfterThisLevel = __BreakEvenAfterThisLevel__;
input bool __HideTP__=false ;    //Hide TakeProfit?
bool HideTP = __HideTP__;
input bool __Use_OPO_Method__=false ;    //Use OPO method to handle TP
bool Use_OPO_Method = __Use_OPO_Method__;
input ENUM_TIMEFRAMES __OPO_TimeFrame__=15  ;    //TF for OPO method
ENUM_TIMEFRAMES OPO_TimeFrame = __OPO_TimeFrame__;
input bool __SmartTP__=false ;    //Smart TakeProfit?
bool SmartTP = __SmartTP__;
input bool __DoNotAdjustTPUnlessNewGrid__=false ;    //Do not adjust TP unless new grid level opened
bool DoNotAdjustTPUnlessNewGrid = __DoNotAdjustTPUnlessNewGrid__;
input string __Strategy_Setting_SL__="Select SL settings"  ;   //------> StopLoss settings <------
string Strategy_Setting_SL = __Strategy_Setting_SL__;
input double __GridSL__=0  ;    //StopLoss for Grid, in pips (1000pips if zero)
double GridSL = __GridSL__;
input bool __HideSL__=false ;    //Hide StopLoss?
bool HideSL = __HideSL__;
input string __Grid_Setting__="Adjust the grid distance and multipliers"  ;   //------> Grid settings <------
string Grid_Setting = __Grid_Setting__;
input int __TradeDistance__=35  ;    //Trade Distance
int TradeDistance = __TradeDistance__;
input bool __SmartDistance__=true  ;    //Smart Distance?
bool SmartDistance = __SmartDistance__;
input double __TradeMultiplier_2nd__=1  ;    //2nd Trade Multiplier
double TradeMultiplier_2nd = __TradeMultiplier_2nd__;
input double __TradeMultiplier_3rd__=2  ;    //3rd-5th Trade Multiplier
double TradeMultiplier_3rd = __TradeMultiplier_3rd__;
input double __TradeMultiplier_6th__=1.5  ;    //6th- Trade Multiplier
double TradeMultiplier_6th = __TradeMultiplier_6th__;
input int __MaximumTrades__=9  ;    //Maximum Trades
int MaximumTrades = __MaximumTrades__;
input int __GridLevelToStart__=1  ;    //Grid Level to Start (1-initial trade)
int GridLevelToStart = __GridLevelToStart__;
input bool __KeepOriginalProfitLotSize__=false ;    //Keep Original Profit Level & Lot Size
bool KeepOriginalProfitLotSize = __KeepOriginalProfitLotSize__;
input string __Additional_Setting__="Change the comment and UID if needed"  ;   //------> Additional settings <------
string Additional_Setting = __Additional_Setting__;
input string __TradeComment__="Waka"  ;   //Trade Comment
string TradeComment = __TradeComment__;
input int __UID__=0  ;    //UID (0...9)
int UID = __UID__;
input bool __ShowPanel__=true  ;    //ShowPanel
bool ShowPanel = __ShowPanel__;
  string    mmm_1_st = "::7318875\\WakaWakaEA.bmp";
  string    mmm_2_st = "2.12";
  long      mmm_3_lo = 0;
  string    mmm_4_st = "";
  int       mmm_5_in = 0;
  string    mmm_6_st = "";
  datetime  mmm_7_da = 0;
  int       mmm_8_in = 0;
  CCanvasX  mmm_10_a_167;
  bool      mmm_11_bo = true;
  int       mmm_12_in = 3000;
  bool      mmm_13_bo = false;
  int       mmm_14_in = 50000;
  CutTrade  mmm_15_a_169_ko[];
  int       mmm_16_in = -1;
  long      mmm_17_lo_ko[];
  double    mmm_18_do_ko[];
  int       mmm_19_in = -1;
  int       mmm_20_in = 0;
  int       mmm_21_in = 15;
  SymbolInformation gainkit[];
  short     mmm_23_sh = 0;
  int       mmm_24_in = 84570;
  double    mmm_25_do = 0.0000001;
  int       mmm_26_in = -1;
  long      mmm_27_lo = 0;
  int       mmm_28_in = 0;
  bool      mmm_29_bo = false;
  int       mmm_30_in = 0;
  bool      mmm_31_bo = false;
  int       mmm_32_in = -1;
  long      mmm_33_lo = 0;
  long      mmm_34_lo = 0;
  bool      mmm_35_bo = false;
  string    mmm_36_st = "Select pair";
  bool      mmm_37_bo = true;
  double    mmm_38_do = 0.0;
  bool      mmm_39_bo = true;
  int       mmm_40_in = 0;

 void OnInit()
 {
  int       nnn_1_in;
  int       nnn_2_in;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  int       nnn_6_in;
  int       nnn_7_in;
  int       nnn_8_in;
  int       nnn_9_in;
  int       nnn_10_in;
  int       nnn_11_in;
  int       nnn_12_in;
  int       nnn_13_in;
  int       nnn_14_in;
  int       nnn_15_in;
  int       nnn_16_in;
  int       nnn_17_in;
  int       nnn_18_in;
  int       nnn_19_in;
  int       nnn_20_in;
  int       nnn_21_in;
  uchar     nnn_22_uc;
  uchar     nnn_23_uc;
  uchar     nnn_24_uc;
  int       nnn_25_in;
  int       nnn_26_in;
  bool      nnn_27_bo;
  string    nnn_28_st_ko[];
  int       nnn_29_in;
  int       nnn_30_in;
  double    nnn_31_do;
  double    nnn_32_do;
  int       nnn_33_in;
  int       nnn_34_in;
//----- -----
 string     ppp_st_1;
 string     ppp_st_2;
 string     ppp_st_3;
 double     ppp_do_4;
 double     ppp_do_5;
 int        ppp_in_6;
 int        ppp_in_7;
 double     ppp_do_8;
 string     ppp_st_9;
 double     ppp_do_10;
 double     ppp_do_11;
 int        ppp_in_12;
 int        ppp_in_13;
 double     ppp_do_14;
 int        ppp_in_15;

 Print(TradeComment + " " + "->",": Initializing..."); 
 mmm_30_in = 0 ;
 mmm_31_bo = false ;
 nnn_2_in = 0 ;
 nnn_3_in = 1 ;
 nnn_4_in=1 + 1;
 nnn_5_in=nnn_4_in + 1;
 nnn_6_in=nnn_4_in + nnn_4_in;
 nnn_7_in=nnn_5_in + nnn_4_in;
 nnn_8_in=nnn_5_in + nnn_5_in;
 nnn_9_in=nnn_6_in + nnn_5_in;
 nnn_10_in=nnn_8_in + nnn_4_in;
 nnn_11_in=nnn_8_in + nnn_5_in;
 nnn_12_in = 0 ;
 nnn_13_in = 1 ;
 nnn_14_in = nnn_4_in ;
 nnn_15_in = nnn_5_in ;
 nnn_16_in=nnn_5_in + 1;
 nnn_17_in=nnn_6_in + 1;
 nnn_18_in=nnn_17_in + 1;
 nnn_19_in=nnn_4_in + nnn_17_in;
 nnn_20_in=nnn_16_in + nnn_16_in;
 nnn_21_in=nnn_20_in + 1;
 for (nnn_22_uc = nnn_19_in * nnn_21_in + nnn_4_in ; nnn_22_uc < nnn_21_in * nnn_11_in + nnn_21_in + nnn_3_in ; nnn_22_uc ++)
 {
   mmm_6_st +=CharToString(nnn_22_uc);
 }
 for (nnn_23_uc = nnn_8_in * nnn_10_in ; nnn_23_uc < nnn_19_in * nnn_10_in + nnn_14_in ; nnn_23_uc ++)
 {
   mmm_6_st +=CharToString(nnn_23_uc);
 }
 for (nnn_24_uc = 97 ; nnn_24_uc < 123 ; nnn_24_uc ++)
 {
   mmm_6_st +=CharToString(nnn_24_uc);
 }
 mmm_6_st +=CharToString(32);
 mmm_6_st +=CharToString(33);
 mmm_6_st +=CharToString(44);
 mmm_6_st +=CharToString(46);
 mmm_6_st +=CharToString(58);
 mmm_6_st +=CharToString(47);
 mmm_6_st +=CharToString(45);
 mmm_6_st +=CharToString(95);
 nnn_25_in = 1 ;
 nnn_26_in = 0 ;
 mmm_3_lo = AccountInfoInteger(ACCOUNT_LOGIN) ;
 mmm_4_st = AccountInfoString(ACCOUNT_NAME) ;
 Sleep(500); 
 if ( !(CFAE::IsTesting()) )
 {
   EventSetTimer(5); 
 }
 mmm_27_lo = TimeCurrent() ;
 mmm_29_bo = false ;
 mmm_23_sh = StringGetCharacter(",",0) ;
 mmm_16_in = -1 ;
 nnn_27_bo = CFAE::IsTesting() ;
 nnn_29_in = StringSplit(Symbols,mmm_23_sh,nnn_28_st_ko) ;
 if ( nnn_29_in >  0 && !(nnn_27_bo) )
 {
   ArrayResize(gainkit,nnn_29_in,0); 
   for (nnn_30_in = 0 ; nnn_30_in < nnn_29_in ; nnn_30_in ++)
   {
     ppp_st_1 = CFAE::StringTrimLeft(nnn_28_st_ko[nnn_30_in]);
     ppp_st_2 = CFAE::StringTrimRight(CFAE::StringTrimLeft(nnn_28_st_ko[nnn_30_in]));
     gainkit[nnn_30_in].st_1 = CFAE::StringTrimRight(CFAE::StringTrimLeft(nnn_28_st_ko[nnn_30_in]));
     if ( gainkit[nnn_30_in].st_1 == "" )
     {
       gainkit[nnn_30_in].st_1 = "??????";
       Print(TradeComment + " " + gainkit[nnn_30_in].st_1,": List of Symbols is incorrect! Check it for extra commas!"); 
       mmm_35_bo = true ;
     }
     gainkit[nnn_30_in].da_2 = 0;
     gainkit[nnn_30_in].in_4 = 0;
     gainkit[nnn_30_in].bo_5 = false;
     gainkit[nnn_30_in].bo_6 = false;
     gainkit[nnn_30_in].da_7 = 0;
     gainkit[nnn_30_in].da_8 = 0;
     gainkit[nnn_30_in].do_9 = 0.0;
     gainkit[nnn_30_in].bo_10 = false;
     gainkit[nnn_30_in].bo_11 = false;
     gainkit[nnn_30_in].do_12 = 1.0;
     gainkit[nnn_30_in].do_13 = 0.0;
     gainkit[nnn_30_in].in_14 = 0;
     gainkit[nnn_30_in].in_15 = 0;
     gainkit[nnn_30_in].lo_16 = 0;
     gainkit[nnn_30_in].do_17 = 0.0;
     gainkit[nnn_30_in].bo_18 = true;
     gainkit[nnn_30_in].bo_19 = true;
     gainkit[nnn_30_in].bo_20 = true;
     gainkit[nnn_30_in].in_21 = 0;
     ppp_st_3 = gainkit[nnn_30_in].st_1;
     ppp_do_4 = 0.1;
     ppp_do_5 = 0.1;
     ppp_in_6 = 1;
     for (ppp_in_7=MaximumTrades - 1 ; ppp_in_6 <= ppp_in_7 ; ppp_in_7=MaximumTrades - 1)
     {
       ppp_do_5 = ppp_do_5 + lizong_36(ppp_st_3,ppp_do_4,ppp_in_6,0.0);
       ppp_in_6=ppp_in_6 + 1;
     }
     if ( ppp_do_4>mmm_25_do )
     {
       ppp_do_8 = ppp_do_5 / ppp_do_4;
     }
     else
     {
       ppp_do_8 = 0.0;
     }
     gainkit[nnn_30_in].do_22 = ppp_do_8;
     gainkit[nnn_30_in].do_23 = 0.0;
     gainkit[nnn_30_in].do_24 = 0.0;
     gainkit[nnn_30_in].do_25 = 0.0;
     gainkit[nnn_30_in].do_26 = 0.0;
   }
 }
 else
 {
   ArrayResize(gainkit,1,0); 
   gainkit[0].st_1 = Symbol();
   gainkit[0].da_2 = 0;
   gainkit[0].in_4 = 0;
   gainkit[0].bo_5 = false;
   gainkit[0].bo_6 = false;
   gainkit[0].da_7 = 0;
   gainkit[0].da_8 = 0;
   gainkit[0].do_9 = 0.0;
   gainkit[0].bo_10 = false;
   gainkit[0].bo_11 = false;
   gainkit[0].do_12 = 1.0;
   gainkit[0].do_13 = 0.0;
   gainkit[0].in_14 = 0;
   gainkit[0].in_15 = 0;
   gainkit[0].lo_16 = 0;
   gainkit[0].do_17 = 0.0;
   gainkit[0].bo_18 = true;
   gainkit[0].bo_19 = true;
   gainkit[0].bo_20 = true;
   gainkit[0].in_21 = 0;
   ppp_st_9 = Symbol();
   ppp_do_10 = 0.1;
   ppp_do_11 = 0.1;
   ppp_in_12 = 1;
   for (ppp_in_13=MaximumTrades - 1 ; ppp_in_12 <= ppp_in_13 ; ppp_in_13=MaximumTrades - 1)
   {
     ppp_do_11 = ppp_do_11 + lizong_36(ppp_st_9,ppp_do_10,ppp_in_12,0.0);
     ppp_in_12=ppp_in_12 + 1;
   }
   if ( ppp_do_10>mmm_25_do )
   {
     ppp_do_14 = ppp_do_11 / ppp_do_10;
   }
   else
   {
     ppp_do_14 = 0.0;
   }
   gainkit[0].do_22 = ppp_do_14;
   gainkit[0].do_23 = 0.0;
   gainkit[0].do_24 = 0.0;
   gainkit[0].do_25 = 0.0;
   gainkit[0].do_26 = 0.0;
 }
 if ( mmm_13_bo )
 {
   ArrayResize(mmm_15_a_169_ko,mmm_14_in,0); 
 }
 if ( !(CFAE::IsOptimization()) )
 {
   CFAE::ObjectsDeleteAll(0,-1); 
   if ( ShowPanel )
   {
     lizong_46(); 
     lizong_49(true); 
   }
   if ( CFAE::IsVisualMode() )
   {
     if ( CFAE::ObjectFind(0,"but_Buy") != -1 && CFAE::ObjectGetInteger(0,"but_Buy",OBJPROP_STATE,0) != 0 )
     {
       lizong_48("but_Buy"); 
     }
     if ( CFAE::ObjectFind(0,"but_Sell") != -1 && CFAE::ObjectGetInteger(0,"but_Sell",OBJPROP_STATE,0) != 0 )
     {
       lizong_48("but_Sell"); 
     }
     if ( CFAE::ObjectFind(0,"but_Pair") != -1 && CFAE::ObjectGetInteger(0,"but_Pair",OBJPROP_STATE,0) != 0 )
     {
       lizong_48("but_Pair"); 
     }
     if ( CFAE::ObjectFind(0,"but_Suspend") != -1 )
     {
       mmm_37_bo=!(CFAE::ObjectGetInteger(0,"but_Suspend",OBJPROP_STATE,0));
       if ( CFAE::ObjectGetInteger(0,"but_Suspend",OBJPROP_STATE,0) == 0 )
       {
         CFAE::ObjectSetInteger(0,"but_Suspend",OBJPROP_BGCOLOR,32768); 
         CFAE::ObjectSetString(0,"but_Suspend",OBJPROP_TEXT,"New grids allowed"); 
       }
       if ( !(mmm_37_bo) )
       {
         CFAE::ObjectSetInteger(0,"but_Suspend",OBJPROP_BGCOLOR,255); 
         CFAE::ObjectSetString(0,"but_Suspend",OBJPROP_TEXT,"New grids NOT allowed!"); 
         for (ppp_in_15 = 0 ; ppp_in_15 < ArraySize(gainkit) ; ppp_in_15=ppp_in_15 + 1)
         {
           gainkit[ppp_in_15].bo_5 = false;
           gainkit[ppp_in_15].bo_6 = false;
         }
       }
       ChartRedraw(0); 
     }
   }
   ChartRedraw(0); 
 }
 if ( mmm_11_bo )
 {
   ArrayResize(mmm_17_lo_ko,mmm_12_in,0); 
   ArrayFill(mmm_17_lo_ko,0,mmm_12_in,0);
   ArrayResize(mmm_18_do_ko,mmm_12_in,0); 
   if ( mmm_12_in != 0 )
   {
     ArrayFill(mmm_18_do_ko,0,mmm_12_in,0.0);
   }
 }
 if ( mmm_11_bo )
 {
   lizong_27(); 
 }
 if ( mmm_11_bo )
 {
   nnn_31_do = 0.0 ;
   nnn_32_do = 0.0 ;
   for (nnn_33_in = 0 ; nnn_33_in < ArraySize(mmm_18_do_ko) ; nnn_33_in ++)
   {
     for (nnn_34_in = 0 ; nnn_34_in < ArraySize(mmm_17_lo_ko) - nnn_33_in - 1 ; nnn_34_in ++)
     {
       if ( mmm_18_do_ko[nnn_34_in]>mmm_18_do_ko[nnn_34_in + 1] )
       {
         nnn_31_do = mmm_18_do_ko[nnn_34_in] ;
         nnn_32_do = mmm_17_lo_ko[nnn_34_in] ;
         mmm_18_do_ko[nnn_34_in] = mmm_18_do_ko[nnn_34_in + 1];
         mmm_17_lo_ko[nnn_34_in] = mmm_17_lo_ko[nnn_34_in + 1];
         mmm_18_do_ko[nnn_34_in + 1] = nnn_31_do;
         mmm_17_lo_ko[nnn_34_in + 1] = nnn_32_do;
       }
     }
   }
 }
 mmm_38_do = AccountInfoDouble(ACCOUNT_BALANCE) ;
 if ( ( nnn_2_in + nnn_3_in + nnn_4_in + nnn_5_in + nnn_6_in + nnn_7_in + nnn_8_in + nnn_9_in + nnn_10_in + nnn_11_in != 45 || nnn_12_in + nnn_13_in + nnn_14_in + nnn_15_in + nnn_16_in + nnn_17_in + nnn_18_in + nnn_19_in + nnn_20_in + nnn_21_in != 45 ) )
 {
   return; 
 }
 return; 
 }
//OnInit <<==--------   --------
 void __OnTick__()
 {
  int       nnn_1_in;
//----- -----
 bool       ppp_bo_1;
 int        ppp_in_2;
 bool       ppp_bo_3;


//-------------------------

 for (nnn_1_in = 0 ; nnn_1_in < ArraySize(gainkit) ; nnn_1_in ++)
 {
   if ( CFAE::iTime(gainkit[nnn_1_in].st_1,mmm_21_in,0) <= gainkit[nnn_1_in].da_2 )
   {
     ppp_bo_1 = false;
   }
   else
   {
     gainkit[nnn_1_in].da_2 = CFAE::iTime(gainkit[nnn_1_in].st_1,mmm_21_in,0);
     ppp_bo_1 = true;
   }
   if ( ppp_bo_1 )
   {
     lizong_32(nnn_1_in); 
     if ( CFAE::IsTradeAllowed() )
     {
       ppp_in_2 = TerminalInfoInteger(8);
       if ( ppp_in_2 != 0 )
       {
         ppp_in_2 = AccountInfoInteger(ACCOUNT_TRADE_EXPERT);
       }
       if ( ppp_in_2 != 0 )
       {
         ppp_in_2 = MQLInfoInteger(MQL_TRADE_ALLOWED);
       }
       if ( ( ppp_in_2 != 0 || CFAE::IsTesting() || CFAE::IsOptimization() ) )
       {
         lizong_37(nnn_1_in); 
         lizong_25(nnn_1_in); 
         lizong_26(nnn_1_in); 
       }
     }
   }
   if ( CFAE::iTime(gainkit[nnn_1_in].st_1,OPO_TimeFrame,0) <= gainkit[nnn_1_in].da_3 )
   {
     ppp_bo_3 = false;
   }
   else
   {
     gainkit[nnn_1_in].da_3 = CFAE::iTime(gainkit[nnn_1_in].st_1,OPO_TimeFrame,0);
     ppp_bo_3 = true;
   }
   if ( ppp_bo_3 )
   {
     gainkit[nnn_1_in].bo_11 = false;
   }
 }
 lizong_35(); 
 }
//OnTick <<==--------   --------
 void OnTimer()
 {
 int        ppp_in_1;

 if ( CFAE::IsTesting() || CFAE::IsOptimization() )   return;
 mmm_27_lo = TimeCurrent() ;
 for (ppp_in_1 = 0 ; ppp_in_1 < ArraySize(gainkit) ; ppp_in_1=ppp_in_1 + 1)
 {
   CFAE::iTime(gainkit[ppp_in_1].st_1,mmm_21_in,0); 
   CFAE::iTime(gainkit[ppp_in_1].st_1,OPO_TimeFrame,0); 
 }
 if ( !(ShowPanel) )   return;
 lizong_49(false); 
 }
//OnTimer <<==--------   --------
 void OnChartEvent( const int uuu_0_in,const long & uuu_1_lo,const double & uuu_2_do,const string & uuu_3_st)
 {
 if ( uuu_0_in != 1 )   return;
 lizong_48(uuu_3_st); 
 }
//OnChartEvent <<==--------   --------
 void OnDeinit( const int uuu_0_in)
 {
 string     ppp_st_1;

 EventKillTimer(); 
 ppp_st_1 = "";
 switch(uuu_0_in)
 {
   case 6 :
   ppp_st_1 = "Account changed";
     break;
   case 3 :
   ppp_st_1 = "Symbol/timeframe changed";
     break;
   case 4 :
   ppp_st_1 = "Chart closed";
     break;
   case 5 :
   ppp_st_1 = "Input parameters changed";
     break;
   case 2 :
   ppp_st_1 = "Expert recompiled";
     break;
   case 1 :
   ppp_st_1 = "Expert removed from the chart";
     break;
   case 7 :
   ppp_st_1 = "New template applied to the chart";
     break;
   default :
   ppp_st_1 = "Expert stopped";
 }
 Print(ppp_st_1); 
 if ( !(CFAE::IsTesting()) && !(CFAE::IsOptimization()) )
 {mmm_10_a_167.Destroy();
 }
 if ( CFAE::IsTesting() || CFAE::IsOptimization() )   return;
 CFAE::ObjectsDeleteAll(0,-1); 
 }
//OnDeinit <<==--------   --------
 int lizong_10( int uuu_0_in)
 {
  int       nnn_1_in;
//----- -----

 switch(uuu_0_in)
 {
   case 0 :
   return(0); 
   case 1 :
   return(1); 
   case 5 :
   return(5); 
   case 15 :
   return(15); 
   case 30 :
   return(30); 
   case 60 :
   return(60); 
   case 240 :
   return(240); 
   case 1440 :
   return(1440); 
   case 10080 :
   return(10080); 
   case 43200 :
   return(43200); 
 }
 return(0); 
 }
//lizong_10 <<==--------   --------
 string lizong_11( int uuu_0_in)
 {
  int       nnn_1_in = 0;
  string    nnn_2_st;
//----- -----
 string     ppp_st_1;

 if ( uuu_0_in == -1 )
 {
   nnn_1_in = CFAE::GetLastError() ;
 }
 else
 {
   nnn_1_in = uuu_0_in ;
 }
 nnn_2_st = " Err.code=" + IntegerToString(nnn_1_in,0,32) + ": " ;
 switch(nnn_1_in)
 {
   case 0 :
   ppp_st_1 = nnn_2_st + "No error returned";
   return(ppp_st_1);
   case 1 :
   ppp_st_1 = nnn_2_st + "No error returned, but the result is unknown";
   return(ppp_st_1);
   case 2 :
   ppp_st_1 = nnn_2_st + "Common error";
   return(ppp_st_1);
   case 3 :
   ppp_st_1 = nnn_2_st + "Invalid trade parameters";
   return(ppp_st_1);
   case 4 :
   ppp_st_1 = nnn_2_st + "Trade server is busy";
   return(ppp_st_1);
   case 5 :
   ppp_st_1 = nnn_2_st + "Old version of the client terminal";
   return(ppp_st_1);
   case 6 :
   ppp_st_1 = nnn_2_st + "No connection with trade server";
   return(ppp_st_1);
   case 7 :
   ppp_st_1 = nnn_2_st + "Not enough rights";
   return(ppp_st_1);
   case 8 :
   ppp_st_1 = nnn_2_st + "Too frequent requests";
   return(ppp_st_1);
   case 9 :
   ppp_st_1 = nnn_2_st + "Malfunctional trade operation";
   return(ppp_st_1);
   case 64 :
   ppp_st_1 = nnn_2_st + "Account disabled";
   return(ppp_st_1);
   case 65 :
   ppp_st_1 = nnn_2_st + "Invalid account";
   return(ppp_st_1);
   case 128 :
   ppp_st_1 = nnn_2_st + "Trade timeout";
   return(ppp_st_1);
   case 129 :
   ppp_st_1 = nnn_2_st + "Invalid price";
   return(ppp_st_1);
   case 130 :
   ppp_st_1 = nnn_2_st + "Invalid stops";
   return(ppp_st_1);
   case 131 :
   ppp_st_1 = nnn_2_st + "Invalid trade volume";
   return(ppp_st_1);
   case 132 :
   ppp_st_1 = nnn_2_st + "Market is closed";
   return(ppp_st_1);
   case 133 :
   ppp_st_1 = nnn_2_st + "Trade is disabled";
   return(ppp_st_1);
   case 134 :
   ppp_st_1 = nnn_2_st + "Not enough money";
   return(ppp_st_1);
   case 135 :
   ppp_st_1 = nnn_2_st + "Price changed";
   return(ppp_st_1);
   case 136 :
   ppp_st_1 = nnn_2_st + "Off quotes";
   return(ppp_st_1);
   case 137 :
   ppp_st_1 = nnn_2_st + "Broker is busy";
   return(ppp_st_1);
   case 138 :
   ppp_st_1 = nnn_2_st + "Requote";
   return(ppp_st_1);
   case 139 :
   ppp_st_1 = nnn_2_st + "Order is locked";
   return(ppp_st_1);
   case 140 :
   ppp_st_1 = nnn_2_st + "Buy orders only allowed";
   return(ppp_st_1);
   case 141 :
   ppp_st_1 = nnn_2_st + "Too many requests";
   return(ppp_st_1);
   case 145 :
   ppp_st_1 = nnn_2_st + "Modification denied because order is too close to market";
   return(ppp_st_1);
   case 146 :
   ppp_st_1 = nnn_2_st + "Trade context is busy";
   return(ppp_st_1);
   case 147 :
   ppp_st_1 = nnn_2_st + "Expirations are denied by broker";
   return(ppp_st_1);
   case 148 :
   ppp_st_1 = nnn_2_st + "The amount of open and pending orders has reached the limit set by the broker";
   return(ppp_st_1);
   case 149 :
   ppp_st_1 = nnn_2_st + "An attempt to open an order opposite to the existing one when hedging is disabled";
   return(ppp_st_1);
   case 150 :
   ppp_st_1 = nnn_2_st + "An attempt to close an order contravening the FIFO rule";
   return(ppp_st_1);
   case 4000 :
   ppp_st_1 = nnn_2_st + "No error returned";
   return(ppp_st_1);
   case 4001 :
   ppp_st_1 = nnn_2_st + "Wrong function pointer";
   return(ppp_st_1);
   case 4002 :
   ppp_st_1 = nnn_2_st + "Array index is out of range";
   return(ppp_st_1);
   case 4003 :
   ppp_st_1 = nnn_2_st + "No memory for function call stack";
   return(ppp_st_1);
   case 4004 :
   ppp_st_1 = nnn_2_st + "Recursive stack overflow";
   return(ppp_st_1);
   case 4005 :
   ppp_st_1 = nnn_2_st + "Not enough stack for parameter";
   return(ppp_st_1);
   case 4006 :
   ppp_st_1 = nnn_2_st + "No memory for parameter string";
   return(ppp_st_1);
   case 4007 :
   ppp_st_1 = nnn_2_st + "No memory for temp string";
   return(ppp_st_1);
   case 4008 :
   ppp_st_1 = nnn_2_st + "Not initialized string";
   return(ppp_st_1);
   case 4009 :
   ppp_st_1 = nnn_2_st + "Not initialized string in array";
   return(ppp_st_1);
   case 4010 :
   ppp_st_1 = nnn_2_st + "No memory for array string";
   return(ppp_st_1);
   case 4011 :
   ppp_st_1 = nnn_2_st + "Too long string";
   return(ppp_st_1);
   case 4012 :
   ppp_st_1 = nnn_2_st + "Remainder from zero divide";
   return(ppp_st_1);
   case 4013 :
   ppp_st_1 = nnn_2_st + "Zero divide";
   return(ppp_st_1);
   case 4014 :
   ppp_st_1 = nnn_2_st + "Unknown command";
   return(ppp_st_1);
   case 4015 :
   ppp_st_1 = nnn_2_st + "Wrong jump (never generated error)";
   return(ppp_st_1);
   case 4016 :
   ppp_st_1 = nnn_2_st + "Not initialized array";
   return(ppp_st_1);
   case 4017 :
   ppp_st_1 = nnn_2_st + "DLL calls are not allowed";
   return(ppp_st_1);
   case 4018 :
   ppp_st_1 = nnn_2_st + "Cannot load library";
   return(ppp_st_1);
   case 4019 :
   ppp_st_1 = nnn_2_st + "Cannot call function";
   return(ppp_st_1);
   case 4020 :
   ppp_st_1 = nnn_2_st + "Expert function calls are not allowed";
   return(ppp_st_1);
   case 4021 :
   ppp_st_1 = nnn_2_st + "Not enough memory for temp string returned from function";
   return(ppp_st_1);
   case 4022 :
   ppp_st_1 = nnn_2_st + " System is busy (never generated error)";
   return(ppp_st_1);
   case 4023 :
   ppp_st_1 = nnn_2_st + "DLL-function call critical error";
   return(ppp_st_1);
   case 4024 :
   ppp_st_1 = nnn_2_st + "Internal error";
   return(ppp_st_1);
   case 4025 :
   ppp_st_1 = nnn_2_st + "Out of memory";
   return(ppp_st_1);
   case 4026 :
   ppp_st_1 = nnn_2_st + "Invalid pointer";
   return(ppp_st_1);
   case 4027 :
   ppp_st_1 = nnn_2_st + "Too many formatters in the format function";
   return(ppp_st_1);
   case 4028 :
   ppp_st_1 = nnn_2_st + "Parameters count exceeds formatters count";
   return(ppp_st_1);
   case 4029 :
   ppp_st_1 = nnn_2_st + "Invalid array";
   return(ppp_st_1);
   case 4030 :
   ppp_st_1 = nnn_2_st + "No reply from chart";
   return(ppp_st_1);
   case 4050 :
   ppp_st_1 = nnn_2_st + "Invalid function parameters count";
   return(ppp_st_1);
   case 4051 :
   ppp_st_1 = nnn_2_st + "Invalid function parameter value";
   return(ppp_st_1);
   case 4052 :
   ppp_st_1 = nnn_2_st + "String function internal error";
   return(ppp_st_1);
   case 4053 :
   ppp_st_1 = nnn_2_st + "Some array error";
   return(ppp_st_1);
   case 4054 :
   ppp_st_1 = nnn_2_st + "Incorrect series array using";
   return(ppp_st_1);
   case 4055 :
   ppp_st_1 = nnn_2_st + "Custom indicator error";
   return(ppp_st_1);
   case 4056 :
   ppp_st_1 = nnn_2_st + "Arrays are incompatible";
   return(ppp_st_1);
   case 4057 :
   ppp_st_1 = nnn_2_st + "Global variables processing error";
   return(ppp_st_1);
   case 4058 :
   ppp_st_1 = nnn_2_st + "Global variable not found";
   return(ppp_st_1);
   case 4059 :
   ppp_st_1 = nnn_2_st + "Function is not allowed in testing mode";
   return(ppp_st_1);
   case 4060 :
   ppp_st_1 = nnn_2_st + "Function is not allowed for call";
   return(ppp_st_1);
   case 4061 :
   ppp_st_1 = nnn_2_st + "Send mail error";
   return(ppp_st_1);
   case 4062 :
   ppp_st_1 = nnn_2_st + "String parameter expected";
   return(ppp_st_1);
   case 4063 :
   ppp_st_1 = nnn_2_st + "Integer parameter expected";
   return(ppp_st_1);
   case 4064 :
   ppp_st_1 = nnn_2_st + "Double parameter expected";
   return(ppp_st_1);
   case 4065 :
   ppp_st_1 = nnn_2_st + "Array as parameter expected";
   return(ppp_st_1);
   case 4066 :
   ppp_st_1 = nnn_2_st + "Requested history data is in updating state";
   return(ppp_st_1);
   case 4067 :
   ppp_st_1 = nnn_2_st + "Internal trade error";
   return(ppp_st_1);
   case 4068 :
   ppp_st_1 = nnn_2_st + "Resource not found";
   return(ppp_st_1);
   case 4069 :
   ppp_st_1 = nnn_2_st + "Resource not supported";
   return(ppp_st_1);
   case 4070 :
   ppp_st_1 = nnn_2_st + "Duplicate resource";
   return(ppp_st_1);
   case 4071 :
   ppp_st_1 = nnn_2_st + "Custom indicator cannot initialize";
   return(ppp_st_1);
   case 4072 :
   ppp_st_1 = nnn_2_st + "Cannot load custom indicator";
   return(ppp_st_1);
   case 4073 :
   ppp_st_1 = nnn_2_st + "No history data";
   return(ppp_st_1);
   case 4074 :
   ppp_st_1 = nnn_2_st + "No memory for history data";
   return(ppp_st_1);
   case 4075 :
   ppp_st_1 = nnn_2_st + "Not enough memory for indicator calculation";
   return(ppp_st_1);
   case 4099 :
   ppp_st_1 = nnn_2_st + "End of file";
   return(ppp_st_1);
   case 4100 :
   ppp_st_1 = nnn_2_st + "Some file error";
   return(ppp_st_1);
   case 4101 :
   ppp_st_1 = nnn_2_st + "Wrong file name";
   return(ppp_st_1);
   case 4102 :
   ppp_st_1 = nnn_2_st + "Too many opened files";
   return(ppp_st_1);
   case 4103 :
   ppp_st_1 = nnn_2_st + "Cannot open file";
   return(ppp_st_1);
   case 4104 :
   ppp_st_1 = nnn_2_st + "Incompatible access to a file";
   return(ppp_st_1);
   case 4105 :
   ppp_st_1 = nnn_2_st + "No order selected";
   return(ppp_st_1);
   case 4106 :
   ppp_st_1 = nnn_2_st + "Unknown symbol";
   return(ppp_st_1);
   case 4107 :
   ppp_st_1 = nnn_2_st + "Invalid price";
   return(ppp_st_1);
   case 4108 :
   ppp_st_1 = nnn_2_st + "Invalid ticket";
   return(ppp_st_1);
   case 4109 :
   ppp_st_1 = nnn_2_st + "Trade is not allowed. Enable checkbox \'Allow live trading\' in the Expert Advisor properties";
   return(ppp_st_1);
   case 4110 :
   ppp_st_1 = nnn_2_st + "Longs are not allowed. Check the Expert Advisor properties";
   return(ppp_st_1);
   case 4111 :
   ppp_st_1 = nnn_2_st + "Shorts are not allowed. Check the Expert Advisor properties";
   return(ppp_st_1);
   case 4112 :
   ppp_st_1 = nnn_2_st + "Automated trading by Expert Advisors/Scripts disabled by trade server";
   return(ppp_st_1);
   case 4200 :
   ppp_st_1 = nnn_2_st + "Object already exists";
   return(ppp_st_1);
   case 4201 :
   ppp_st_1 = nnn_2_st + "Unknown object property";
   return(ppp_st_1);
   case 4202 :
   ppp_st_1 = nnn_2_st + "Object does not exist";
   return(ppp_st_1);
   case 4203 :
   ppp_st_1 = nnn_2_st + "Unknown object type";
   return(ppp_st_1);
   case 4204 :
   ppp_st_1 = nnn_2_st + "No object name";
   return(ppp_st_1);
   case 4205 :
   ppp_st_1 = nnn_2_st + "Object coordinates error";
   return(ppp_st_1);
   case 4206 :
   ppp_st_1 = nnn_2_st + "No specified subwindow";
   return(ppp_st_1);
   case 4207 :
   ppp_st_1 = nnn_2_st + "Graphical object error";
   return(ppp_st_1);
   case 4210 :
   ppp_st_1 = nnn_2_st + "Unknown chart property";
   return(ppp_st_1);
   case 4211 :
   ppp_st_1 = nnn_2_st + "Chart not found";
   return(ppp_st_1);
   case 4212 :
   ppp_st_1 = nnn_2_st + "Chart subwindow not found";
   return(ppp_st_1);
   case 4213 :
   ppp_st_1 = nnn_2_st + "Chart indicator not found";
   return(ppp_st_1);
   case 4220 :
   ppp_st_1 = nnn_2_st + "Symbol select error";
   return(ppp_st_1);
   case 4250 :
   ppp_st_1 = nnn_2_st + "Notification error";
   return(ppp_st_1);
   case 4251 :
   ppp_st_1 = nnn_2_st + "Notification parameter error";
   return(ppp_st_1);
   case 4252 :
   ppp_st_1 = nnn_2_st + "Notifications disabled";
   return(ppp_st_1);
   case 4253 :
   ppp_st_1 = nnn_2_st + "Notification send too frequent";
   return(ppp_st_1);
   case 4260 :
   ppp_st_1 = nnn_2_st + "FTP server is not specified";
   return(ppp_st_1);
   case 4261 :
   ppp_st_1 = nnn_2_st + "FTP login is not specified";
   return(ppp_st_1);
   case 4262 :
   ppp_st_1 = nnn_2_st + "FTP connection failed";
   return(ppp_st_1);
   case 4263 :
   ppp_st_1 = nnn_2_st + "FTP connection closed";
   return(ppp_st_1);
   case 4264 :
   ppp_st_1 = nnn_2_st + "FTP path not found on server";
   return(ppp_st_1);
   case 4265 :
   ppp_st_1 = nnn_2_st + "File not found in the MQL4\\Files directory to send on FTP server";
   return(ppp_st_1);
   case 4266 :
   ppp_st_1 = nnn_2_st + "Common error during FTP data transmission";
   return(ppp_st_1);
   case 5001 :
   ppp_st_1 = nnn_2_st + "Too many opened files";
   return(ppp_st_1);
   case 5002 :
   ppp_st_1 = nnn_2_st + "Wrong file name";
   return(ppp_st_1);
   case 5003 :
   ppp_st_1 = nnn_2_st + "Too long file name";
   return(ppp_st_1);
   case 5004 :
   ppp_st_1 = nnn_2_st + "Cannot open file";
   return(ppp_st_1);
   case 5005 :
   ppp_st_1 = nnn_2_st + "Text file buffer allocation error";
   return(ppp_st_1);
   case 5006 :
   ppp_st_1 = nnn_2_st + "Cannot delete file";
   return(ppp_st_1);
   case 5007 :
   ppp_st_1 = nnn_2_st + "Invalid file handle (file closed or was not opened)";
   return(ppp_st_1);
   case 5008 :
   ppp_st_1 = nnn_2_st + "Wrong file handle (handle index is out of handle table)";
   return(ppp_st_1);
   case 5009 :
   ppp_st_1 = nnn_2_st + "File must be opened with FILE_WRITE flag";
   return(ppp_st_1);
   case 5010 :
   ppp_st_1 = nnn_2_st + "File must be opened with FILE_READ flag";
   return(ppp_st_1);
   case 5011 :
   ppp_st_1 = nnn_2_st + "File must be opened with FILE_BIN flag";
   return(ppp_st_1);
   case 5012 :
   ppp_st_1 = nnn_2_st + "File must be opened with FILE_TXT flag";
   return(ppp_st_1);
   case 5013 :
   ppp_st_1 = nnn_2_st + "File must be opened with FILE_TXT or FILE_CSV flag";
   return(ppp_st_1);
   case 5014 :
   ppp_st_1 = nnn_2_st + "File must be opened with FILE_CSV flag";
   return(ppp_st_1);
   case 5015 :
   ppp_st_1 = nnn_2_st + "File read error";
   return(ppp_st_1);
   case 5016 :
   ppp_st_1 = nnn_2_st + "File write error";
   return(ppp_st_1);
   case 5017 :
   ppp_st_1 = nnn_2_st + "String size must be specified for binary file";
   return(ppp_st_1);
   case 5018 :
   ppp_st_1 = nnn_2_st + "Incompatible file (for string arrays-TXT, for others-BIN)";
   return(ppp_st_1);
   case 5019 :
   ppp_st_1 = nnn_2_st + "File is directory not file";
   return(ppp_st_1);
   case 5020 :
   ppp_st_1 = nnn_2_st + "File does not exist";
   return(ppp_st_1);
   case 5021 :
   ppp_st_1 = nnn_2_st + "File cannot be rewritten";
   return(ppp_st_1);
   case 5022 :
   ppp_st_1 = nnn_2_st + "Wrong directory name";
   return(ppp_st_1);
   case 5023 :
   ppp_st_1 = nnn_2_st + "Directory does not exist";
   return(ppp_st_1);
   case 5024 :
   ppp_st_1 = nnn_2_st + "Specified file is not directory";
   return(ppp_st_1);
   case 5025 :
   ppp_st_1 = nnn_2_st + "Cannot delete directory";
   return(ppp_st_1);
   case 5026 :
   ppp_st_1 = nnn_2_st + "Cannot clean directory";
   return(ppp_st_1);
   case 5027 :
   ppp_st_1 = nnn_2_st + "Array resize error";
   return(ppp_st_1);
   case 5028 :
   ppp_st_1 = nnn_2_st + "String resize error";
   return(ppp_st_1);
   case 5029 :
   ppp_st_1 = nnn_2_st + "Structure contains strings or dynamic arrays";
   return(ppp_st_1);
   case 5200 :
   ppp_st_1 = nnn_2_st + "Invalid URL";
   return(ppp_st_1);
   case 5201 :
   ppp_st_1 = nnn_2_st + "Failed to connect to specified URL";
   return(ppp_st_1);
   case 5202 :
   ppp_st_1 = nnn_2_st + "Timeout exceeded";
   return(ppp_st_1);
   case 5203 :
   ppp_st_1 = nnn_2_st + "HTTP request failed";
   return(ppp_st_1);
 }
 ppp_st_1 = nnn_2_st + "Unknown error number";
 return(ppp_st_1);
 }
//lizong_11 <<==--------   --------
 bool CCanvasX::CCanvasX_12( string uuu_0_st)
 {
  bool      nnn_2_bo;
  int       nnn_3_in;
  string    nnn_4_st;
  int       nnn_5_in;
  int       nnn_6_in = 0;
  int       nnn_7_in = 0;
  int       nnn_8_in = 0;
  int       nnn_9_in = 0;
  CFileBin  nnn_10_a_162;
//----- -----

 nnn_5_in = -1 ;
 nnn_4_st = "" ;
 nnn_3_in = 32 ;
 if ( !(ResourceReadImage(uuu_0_st,m_pixels,m_width,m_height)) )
 {
    if ( nnn_5_in != -1 )
   {
     FileClose(nnn_5_in); 
     nnn_5_in = -1 ;
     nnn_4_st = "" ;
     nnn_3_in &=96;
   }
   ; 
 }
// return(true); 
 if ( nnn_5_in != -1 )
 {
   FileClose(nnn_5_in); 
   nnn_5_in = -1 ;
   nnn_4_st = "" ;
   nnn_3_in &=96;
 }
 return(true); 
 }
//CCanvasX_12 <<==--------   --------
 void SymbolInformation::SymbolInformation_13()
 {
 }
//SymbolInformation_13 <<==--------   --------
 void SymbolInformation::SymbolInformation_14()
 {
 }
//SymbolInformation_14 <<==--------   --------
 void SymbolInformation::SymbolInformation_15()
 {
 SymbolInformation_13(); 
 SymbolInformation_14(); 
 }
//SymbolInformation_15 <<==--------   --------
 void SymbolInformation::~SymbolInformation()
 {
/*
*/
 }
//~SymbolInformation <<==--------   --------
 void CutTrade::CutTrade_17()
 {
 }
//CutTrade_17 <<==--------   --------
 void CutTrade::CutTrade_18()
 {
 }
//CutTrade_18 <<==--------   --------
 void CutTrade::CutTrade_19()
 {
 CutTrade_17(); 
 CutTrade_18(); 
 }
//CutTrade_19 <<==--------   --------
 void CutTrade::~CutTrade()
 {
/*
*/
 }
//~CutTrade <<==--------   --------
 bool lizong_21( string uuu_0_st,int uuu_1_in,int uuu_2_in)
 {
  bool      nnn_1_bo;
  bool      nnn_2_bo = false;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  int       nnn_6_in;
  int       nnn_7_in;
  int       nnn_8_in;
  int       nnn_9_in;
  int       nnn_10_in;
  int       nnn_11_in;
  int       nnn_12_in;
  int       nnn_13_in;
  int       nnn_14_in;
  string    nnn_15_st;
  int       nnn_16_in;
  int       nnn_17_in;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;
 int        ppp_in_3;
 int        ppp_in_4;

 nnn_3_in=mmm_24_in + UID;
 nnn_4_in=StringLen(IntegerToString(nnn_3_in,0,32)); 
 nnn_5_in=nnn_3_in + int(MathPow(10.0,nnn_4_in));
 nnn_6_in=nnn_3_in + int(MathPow(10.0,nnn_4_in)) * 2;
 nnn_7_in = -1 ;
 nnn_8_in = -1 ;
 nnn_9_in = -1 ;
 nnn_10_in = -1 ;
 nnn_11_in = -1 ;
 nnn_12_in = -1 ;
 if ( uuu_2_in == 1 )
 {
   nnn_7_in = 0 ;
   nnn_8_in = 0 ;
   if ( uuu_1_in >= 0 )
   {
     nnn_9_in=int(MathPow(10.0,StringLen(IntegerToString(nnn_3_in,0,32))  + 2)) + nnn_3_in * 100 + uuu_1_in;
     nnn_10_in = nnn_9_in ;
   }
   else
   {
     nnn_11_in = nnn_5_in ;
     nnn_12_in = nnn_5_in ;
   }
 }
 if ( uuu_2_in == -1 )
 {
   nnn_7_in = 1 ;
   nnn_8_in = 1 ;
   if ( uuu_1_in >= 0 )
   {
     nnn_9_in=(int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32))  + 2))) * 2 + (mmm_24_in + UID) * 100 + uuu_1_in;
     nnn_10_in = nnn_9_in ;
   }
   else
   {
     nnn_11_in = nnn_6_in ;
     nnn_12_in = nnn_6_in ;
   }
 }
 if ( uuu_2_in == 0 )
 {
   nnn_7_in = 0 ;
   nnn_8_in = 1 ;
   if ( uuu_1_in >= 0 )
   {
     nnn_9_in=int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32))  + 2)) + (mmm_24_in + UID) * 100 + uuu_1_in;
     if ( uuu_1_in <  0 )
     {
       ppp_in_1 = -1;
     }
     else
     {
       ppp_in_2 = mmm_24_in + UID;
       ppp_in_3 = StringLen(IntegerToString(ppp_in_2,0,32)) ;
       ppp_in_4 = 0;
       if ( -1 == 1 )
       {
         ppp_in_4 = 1;
       }
       if ( -1 == -1 )
       {
         ppp_in_4 = 2;
       }
       ppp_in_1 = int(MathPow(10.0,ppp_in_3 + 2)) * ppp_in_4 + ppp_in_2 * 100 + uuu_1_in;
     }
     nnn_10_in = ppp_in_1 ;
   }
   else
   {
     nnn_11_in = nnn_5_in ;
     nnn_12_in = nnn_6_in ;
   }
 }
 for (nnn_13_in = 0 ; nnn_13_in < CFAE::OrdersTotal() ; nnn_13_in ++)
 {
   if ( CFAE::OrderSelect(nnn_13_in,0,0) )
   {
     nnn_14_in = CFAE::OrderType() ;
     nnn_15_st = CFAE::OrderSymbol() ;
     nnn_16_in = CFAE::OrderMagicNumber() ;
     nnn_17_in=nnn_16_in / 100;
     if ( uuu_1_in >= 0 && nnn_15_st == uuu_0_st && ( ( nnn_16_in == nnn_9_in && nnn_14_in == nnn_7_in ) || (nnn_16_in == nnn_10_in && nnn_14_in == nnn_8_in) ) )
     {
       return(true); 
     }
     if ( uuu_1_in <  0 && nnn_15_st == uuu_0_st && ( ( nnn_17_in == nnn_11_in && nnn_14_in == nnn_7_in ) || (nnn_17_in == nnn_12_in && nnn_14_in == nnn_8_in) ) )
     {
       return(true); 
     }
   }
   else
   {
     Print(TradeComment + " " + uuu_0_st,": Failed to select an order! Error=",lizong_11(CFAE::GetLastError())); 
     nnn_2_bo = true ;
   }
 }
 return(nnn_2_bo); 
 }
//lizong_21 <<==--------   --------
 double lizong_22( string uuu_0_st,int uuu_1_in,int uuu_2_in)
 {
  double    nnn_1_do;
  double    nnn_2_do = 0.0;
  int       nnn_3_in;
  int       nnn_4_in;
  double    nnn_5_do;
  double    nnn_6_do;
  int       nnn_7_in;
  int       nnn_8_in;
  string    nnn_9_st;
  int       nnn_10_in;
  double    nnn_11_do;
  double    nnn_12_do;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;
 int        ppp_in_3;
 int        ppp_in_4;
 int        ppp_in_5;

 ppp_in_1 = uuu_2_in;
 if ( uuu_1_in <  0 )
 {
   ppp_in_2 = -1;
 }
 else
 {
   ppp_in_3 = mmm_24_in + UID;
   ppp_in_4 = StringLen(IntegerToString(ppp_in_3,0,32)) ;
   ppp_in_5 = 0;
   if ( ppp_in_1 == 1 )
   {
     ppp_in_5 = 1;
   }
   if ( ppp_in_1 == -1 )
   {
     ppp_in_5 = 2;
   }
   ppp_in_2 = int(MathPow(10.0,ppp_in_4 + 2)) * ppp_in_5 + ppp_in_3 * 100 + uuu_1_in;
 }
 nnn_3_in = ppp_in_2 ;
 nnn_4_in = -1 ;
 if ( uuu_2_in == 1 )
 {
   nnn_4_in = 0 ;
 }
 if ( uuu_2_in == -1 )
 {
   nnn_4_in = 1 ;
 }
 nnn_5_do = 0.0 ;
 nnn_6_do = 0.0 ;
 for (nnn_7_in = 0 ; nnn_7_in < CFAE::OrdersTotal() ; nnn_7_in ++)
 {
   if ( CFAE::OrderSelect(nnn_7_in,0,0) )
   {
     nnn_8_in = CFAE::OrderType() ;
     nnn_9_st = CFAE::OrderSymbol() ;
     nnn_10_in = CFAE::OrderMagicNumber() ;
     nnn_11_do = CFAE::OrderOpenPrice() ;
     nnn_12_do = CFAE::OrderLots() ;
     if ( nnn_9_st == uuu_0_st && nnn_10_in == nnn_3_in && nnn_8_in == nnn_4_in )
     {
       nnn_6_do = nnn_11_do * nnn_12_do + nnn_6_do ;
       nnn_5_do = nnn_5_do + nnn_12_do ;
       if ( !(AutoSplit) )
       {
         break;
       }
     }
   }
   else
   {
     Print(TradeComment + " " + uuu_0_st,": Failed to select an order! Error=",lizong_11(CFAE::GetLastError())); 
   }
 }
 if ( nnn_5_do>mmm_25_do )
 {
   nnn_2_do = nnn_6_do / nnn_5_do ;
 }
 return(nnn_2_do); 
 }
//lizong_22 <<==--------   --------
 double lizong_23( string uuu_0_st,int uuu_1_in,bool uuu_2_bo,bool uuu_3_bo)
 {
  double    nnn_1_do;
  double    nnn_2_do = 0.0;
  double    nnn_3_do = 0.0;
  double    nnn_4_do = 0.0;
  int       nnn_5_in;
  int       nnn_6_in;
  int       nnn_7_in;
  int       nnn_8_in;
  double    nnn_9_do;
  int       nnn_10_in;
  string    nnn_11_st;
  int       nnn_12_in;
  int       nnn_13_in;
  double    nnn_14_do;
  double    nnn_15_do;
  double    nnn_16_do;
  int       nnn_17_in;
  int       nnn_18_in;
  string    nnn_19_st;
  int       nnn_20_in;
  double    nnn_21_do;
  double    nnn_22_do;
  double    nnn_23_do;
  double    nnn_24_do;
  double    nnn_25_do;
//----- -----
 int        ppp_in_1;
 double     ppp_do_2;
 int        ppp_in_3;
 double     ppp_do_4;
 int        ppp_in_5;
 double     ppp_do_6;
 double     ppp_do_7;
 int        ppp_in_8;
 double     ppp_do_9;
 int        ppp_in_10;
 double     ppp_do_11;
 int        ppp_in_12;
 double     ppp_do_13;
 int        ppp_in_14;

 nnn_5_in=mmm_24_in + UID;
 nnn_6_in=StringLen(IntegerToString(nnn_5_in,0,32)); 
 nnn_7_in = 0 ;
 nnn_8_in = -1 ;
 if ( uuu_1_in == 1 )
 {
   nnn_8_in = 0 ;
   nnn_7_in = 1 ;
 }
 if ( uuu_1_in == -1 )
 {
   nnn_8_in = 1 ;
   nnn_7_in = 2 ;
 }
 nnn_9_do = 0.0 ;
 if ( KeepOriginalProfitLotSize && uuu_3_bo && GridLevelToStart >  1 && !(AutoSplit) )
 {
   for (nnn_10_in = 0 ; nnn_10_in < CFAE::OrdersTotal() ; nnn_10_in ++)
   {
     if ( CFAE::OrderSelect(nnn_10_in,0,0) )
     {
       nnn_11_st = CFAE::OrderSymbol() ;
       nnn_12_in = CFAE::OrderType() ;
       nnn_13_in = CFAE::OrderMagicNumber() ;
       nnn_14_do = CFAE::OrderLots() ;
       if ( nnn_11_st == uuu_0_st && nnn_13_in / 100 == nnn_5_in + int(MathPow(10.0,nnn_6_in)) * nnn_7_in && nnn_12_in == nnn_8_in )
       {
         nnn_15_do=nnn_13_in - nnn_13_in / 100 * 100;
         if ( nnn_15_do >= GridLevelToStart - 1 && nnn_14_do>mmm_25_do )
         {
           nnn_9_do = nnn_14_do ;
           ppp_in_1 = nnn_15_do;
           ppp_do_2 = 1.0;
           for (ppp_in_3 = 1 ; ppp_in_3 <= ppp_in_1 ; ppp_in_3=ppp_in_3 + 1)
           {
             if ( ppp_in_3 == 1 )
             {
               ppp_do_2 = TradeMultiplier_2nd;
             }
             if ( ppp_in_3 >= 2 && ppp_in_3 <= 4 )
             {
               ppp_do_2 = ppp_do_2 * TradeMultiplier_3rd;
             }
             if ( ppp_in_3 >= 5 )
             {
               ppp_do_2 = ppp_do_2 * TradeMultiplier_6th;
             }
           }
           nnn_16_do = ppp_do_2 ;
           if ( nnn_16_do>mmm_25_do )
           {
             nnn_9_do = nnn_9_do / nnn_16_do ;
           }
           if ( nnn_9_do>mmm_25_do )
           {
             break;
           }
         }
       }
     }
     else
     {
       Print(TradeComment + " " + uuu_0_st,": Failed to select an order! Error=",lizong_11(CFAE::GetLastError())); 
     }
   }
 }
 for (nnn_17_in = 0 ; nnn_17_in < CFAE::OrdersTotal() ; nnn_17_in ++)
 {
   if ( CFAE::OrderSelect(nnn_17_in,0,0) )
   {
     nnn_18_in = CFAE::OrderType() ;
     nnn_19_st = CFAE::OrderSymbol() ;
     nnn_20_in = CFAE::OrderMagicNumber() ;
     nnn_21_do = CFAE::OrderLots() ;
     nnn_22_do = CFAE::OrderOpenPrice() ;
     if ( nnn_19_st == uuu_0_st && nnn_20_in / 100 == nnn_5_in + int(MathPow(10.0,nnn_6_in)) * nnn_7_in && nnn_18_in == nnn_8_in )
     {
       nnn_23_do = nnn_22_do ;
       if ( uuu_2_bo )
       {
         ppp_do_4 = 0.0;
         if ( CFAE::MarketInfo(uuu_0_st,16) * nnn_21_do>mmm_25_do )
         {
           ppp_in_5 = CFAE::MarketInfo(uuu_0_st,12);
           ppp_do_6 = (CFAE::OrderCommission() + CFAE::OrderSwap()) / (CFAE::MarketInfo(uuu_0_st,16) * nnn_21_do);
           if ( CFAE::MarketInfo(uuu_0_st,11)>mmm_25_do )
           {
             ppp_do_7 = CFAE::MarketInfo(uuu_0_st,11);
           }
           else
           {
             ppp_do_7 = 0.00001;
           }
           ppp_do_6 = ppp_do_6 * ppp_do_7;
           ppp_do_4 = NormalizeDouble(ppp_do_6,ppp_in_5);
         }
         nnn_24_do = ppp_do_4 ;
         if ( uuu_1_in == 1 )
         {
           ppp_in_8 = CFAE::MarketInfo(uuu_0_st,12);
           if ( CFAE::MarketInfo(uuu_0_st,11)>mmm_25_do )
           {
             ppp_do_9 = CFAE::MarketInfo(uuu_0_st,11);
           }
           else
           {
             ppp_do_9 = 0.00001;
           }
           nnn_23_do = NormalizeDouble(nnn_22_do + ppp_do_9 - nnn_24_do,ppp_in_8) ;
         }
         if ( uuu_1_in == -1 )
         {
           ppp_in_10 = CFAE::MarketInfo(uuu_0_st,12);
           if ( CFAE::MarketInfo(uuu_0_st,11)>mmm_25_do )
           {
             ppp_do_11 = CFAE::MarketInfo(uuu_0_st,11);
           }
           else
           {
             ppp_do_11 = 0.00001;
           }
           nnn_23_do = NormalizeDouble(nnn_22_do - ppp_do_11 + nnn_24_do,ppp_in_10) ;
         }
       }
       if ( KeepOriginalProfitLotSize && uuu_3_bo && GridLevelToStart >  1 && nnn_9_do>mmm_25_do && !(AutoSplit) )
       {
         nnn_25_do=nnn_20_in - nnn_20_in / 100 * 100;
         if ( nnn_25_do == 0.0 )
         {
           nnn_21_do = nnn_9_do ;
         }
         if ( nnn_25_do >  0 )
         {
           ppp_in_12 = nnn_25_do;
           ppp_do_13 = 1.0;
           for (ppp_in_14 = 1 ; ppp_in_14 <= ppp_in_12 ; ppp_in_14=ppp_in_14 + 1)
           {
             if ( ppp_in_14 == 1 )
             {
               ppp_do_13 = TradeMultiplier_2nd;
             }
             if ( ppp_in_14 >= 2 && ppp_in_14 <= 4 )
             {
               ppp_do_13 = ppp_do_13 * TradeMultiplier_3rd;
             }
             if ( ppp_in_14 >= 5 )
             {
               ppp_do_13 = ppp_do_13 * TradeMultiplier_6th;
             }
           }
           nnn_21_do = nnn_9_do * ppp_do_13 ;
         }
       }
       nnn_3_do = nnn_23_do * nnn_21_do + nnn_3_do ;
       nnn_4_do = nnn_4_do + nnn_21_do ;
     }
   }
   else
   {
     Print(TradeComment + " " + uuu_0_st,": Failed to select an order! Error=",lizong_11(CFAE::GetLastError())); 
   }
 }
 if ( nnn_4_do>mmm_25_do )
 {
   nnn_2_do = nnn_3_do / nnn_4_do ;
 }
 nnn_2_do = NormalizeDouble(nnn_2_do,CFAE::MarketInfo(uuu_0_st,12)) ;
 return(nnn_2_do); 
 }
//lizong_23 <<==--------   --------
 double lizong_24( string uuu_0_st,int uuu_1_in,int uuu_2_in,bool uuu_3_bo)
 {
  double    nnn_1_do;
  double    nnn_2_do = 0.0;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  int       nnn_6_in;
  int       nnn_7_in;
  int       nnn_8_in;
  int       nnn_9_in;
  int       nnn_10_in;
  int       nnn_11_in;
  int       nnn_12_in;
  int       nnn_13_in;
  int       nnn_14_in;
  double    nnn_15_do;
  int       nnn_16_in;
  int       nnn_17_in;
  string    nnn_18_st;
  int       nnn_19_in;
  double    nnn_20_do;
  int       nnn_21_in;
  double    nnn_22_do;
  double    nnn_23_do;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;
 int        ppp_in_3;
 int        ppp_in_4;
 int        ppp_in_5;
 double     ppp_do_6;
 int        ppp_in_7;
 int        ppp_in_8;
 double     ppp_do_9;
 int        ppp_in_10;

 nnn_3_in=mmm_24_in + UID;
 nnn_4_in=StringLen(IntegerToString(nnn_3_in,0,32)); 
 nnn_5_in=nnn_3_in + int(MathPow(10.0,nnn_4_in));
 nnn_6_in=nnn_3_in + int(MathPow(10.0,nnn_4_in)) * 2;
 nnn_7_in = -1 ;
 nnn_8_in = -1 ;
 nnn_9_in = -1 ;
 nnn_10_in = -1 ;
 nnn_11_in = -1 ;
 nnn_12_in = -1 ;
 if ( uuu_2_in == 1 )
 {
   nnn_7_in = 0 ;
   nnn_8_in = 0 ;
   if ( uuu_1_in >= 0 )
   {
     nnn_9_in=int(MathPow(10.0,StringLen(IntegerToString(nnn_3_in,0,32))  + 2)) + nnn_3_in * 100 + uuu_1_in;
     nnn_10_in = nnn_9_in ;
   }
   else
   {
     nnn_11_in = nnn_5_in ;
     nnn_12_in = nnn_5_in ;
   }
 }
 if ( uuu_2_in == -1 )
 {
   nnn_7_in = 1 ;
   nnn_8_in = 1 ;
   if ( uuu_1_in >= 0 )
   {
     nnn_9_in=(int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32))  + 2))) * 2 + (mmm_24_in + UID) * 100 + uuu_1_in;
     nnn_10_in = nnn_9_in ;
   }
   else
   {
     nnn_11_in = nnn_6_in ;
     nnn_12_in = nnn_6_in ;
   }
 }
 if ( uuu_2_in == 0 )
 {
   nnn_7_in = 0 ;
   nnn_8_in = 1 ;
   if ( uuu_1_in >= 0 )
   {
     nnn_9_in=int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32))  + 2)) + (mmm_24_in + UID) * 100 + uuu_1_in;
     if ( uuu_1_in <  0 )
     {
       ppp_in_1 = -1;
     }
     else
     {
       ppp_in_2 = mmm_24_in + UID;
       ppp_in_3 = StringLen(IntegerToString(ppp_in_2,0,32)) ;
       ppp_in_4 = 0;
       if ( -1 == 1 )
       {
         ppp_in_4 = 1;
       }
       if ( -1 == -1 )
       {
         ppp_in_4 = 2;
       }
       ppp_in_1 = int(MathPow(10.0,ppp_in_3 + 2)) * ppp_in_4 + ppp_in_2 * 100 + uuu_1_in;
     }
     nnn_10_in = ppp_in_1 ;
   }
   else
   {
     nnn_11_in = nnn_5_in ;
     nnn_12_in = nnn_6_in ;
   }
 }
 nnn_13_in = 0 ;
 nnn_14_in = -1 ;
 if ( uuu_2_in == 1 )
 {
   nnn_14_in = 0 ;
   nnn_13_in = 1 ;
 }
 if ( uuu_2_in == -1 )
 {
   nnn_14_in = 1 ;
   nnn_13_in = 2 ;
 }
 nnn_15_do = 0.0 ;
 if ( KeepOriginalProfitLotSize && uuu_3_bo && GridLevelToStart >  1 && !(AutoSplit) )
 {
   nnn_15_do = 0.01 ;
 }
 for (nnn_16_in = 0 ; nnn_16_in < CFAE::OrdersTotal() ; nnn_16_in ++)
 {
   if ( CFAE::OrderSelect(nnn_16_in,0,0) )
   {
     nnn_17_in = CFAE::OrderType() ;
     nnn_18_st = CFAE::OrderSymbol() ;
     nnn_19_in = CFAE::OrderMagicNumber() ;
     nnn_20_do = CFAE::OrderLots() ;
     nnn_21_in=nnn_19_in / 100;
     if ( uuu_1_in >= 0 && nnn_18_st == uuu_0_st && ( ( nnn_19_in == nnn_9_in && nnn_17_in == nnn_7_in ) || (nnn_19_in == nnn_10_in && nnn_17_in == nnn_8_in) ) )
     {
       if ( !(uuu_3_bo) )
       {
         nnn_2_do = nnn_2_do + nnn_20_do ;
       }
       else
       {
         if ( KeepOriginalProfitLotSize && uuu_3_bo && GridLevelToStart >  1 && nnn_15_do>mmm_25_do && !(AutoSplit) )
         {
           nnn_22_do=nnn_19_in - nnn_19_in / 100 * 100;
           if ( nnn_22_do == 0.0 )
           {
             nnn_20_do = nnn_15_do ;
           }
           if ( nnn_22_do >  0 )
           {
             ppp_in_5 = nnn_22_do;
             ppp_do_6 = 1.0;
             for (ppp_in_7 = 1 ; ppp_in_7 <= ppp_in_5 ; ppp_in_7=ppp_in_7 + 1)
             {
               if ( ppp_in_7 == 1 )
               {
                 ppp_do_6 = TradeMultiplier_2nd;
               }
               if ( ppp_in_7 >= 2 && ppp_in_7 <= 4 )
               {
                 ppp_do_6 = ppp_do_6 * TradeMultiplier_3rd;
               }
               if ( ppp_in_7 >= 5 )
               {
                 ppp_do_6 = ppp_do_6 * TradeMultiplier_6th;
               }
             }
             nnn_20_do = nnn_15_do * ppp_do_6 ;
           }
         }
         nnn_2_do = nnn_2_do + nnn_20_do ;
       }
       if ( !(AutoSplit) )
       {
         break;
       }
     }
     if ( uuu_1_in <  0 && nnn_18_st == uuu_0_st && ( ( nnn_21_in == nnn_11_in && nnn_17_in == nnn_7_in ) || (nnn_21_in == nnn_12_in && nnn_17_in == nnn_8_in) ) )
     {
       if ( !(uuu_3_bo) )
       {
         nnn_2_do = nnn_2_do + nnn_20_do ;
       }
       else
       {
         if ( KeepOriginalProfitLotSize && uuu_3_bo && GridLevelToStart >  1 && nnn_15_do>mmm_25_do && !(AutoSplit) )
         {
           nnn_23_do=nnn_19_in - nnn_19_in / 100 * 100;
           if ( nnn_23_do == 0.0 )
           {
             nnn_20_do = nnn_15_do ;
           }
           if ( nnn_23_do >  0 )
           {
             ppp_in_8 = nnn_23_do;
             ppp_do_9 = 1.0;
             for (ppp_in_10 = 1 ; ppp_in_10 <= ppp_in_8 ; ppp_in_10=ppp_in_10 + 1)
             {
               if ( ppp_in_10 == 1 )
               {
                 ppp_do_9 = TradeMultiplier_2nd;
               }
               if ( ppp_in_10 >= 2 && ppp_in_10 <= 4 )
               {
                 ppp_do_9 = ppp_do_9 * TradeMultiplier_3rd;
               }
               if ( ppp_in_10 >= 5 )
               {
                 ppp_do_9 = ppp_do_9 * TradeMultiplier_6th;
               }
             }
             nnn_20_do = nnn_15_do * ppp_do_9 ;
           }
         }
         nnn_2_do = nnn_2_do + nnn_20_do ;
       }
     }
   }
   else
   {
     Print(TradeComment + " " + uuu_0_st,": Failed to select an order! Error=",lizong_11(CFAE::GetLastError())); 
   }
 }
 return(nnn_2_do); 
 }
//lizong_24 <<==--------   --------
 void lizong_25( int uuu_0_in)
 {
  string    nnn_1_st;
  int       nnn_2_in;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  int       nnn_6_in;
  int       nnn_7_in;
  int       nnn_8_in;
  int       nnn_9_in;
  string    nnn_10_st;
  double    nnn_11_do;
  int       nnn_12_in;
  double    nnn_13_do;
  double    nnn_14_do;
  double    nnn_15_do;
  double    nnn_16_do;
  double    nnn_17_do;
//----- -----
 double     ppp_do_1;
 int        ppp_in_2;
 double     ppp_do_3;
 double     ppp_do_4;

 if ( CFAE::OrdersTotal() == 0 )   return;
 nnn_1_st = gainkit[uuu_0_in].st_1 ;
 nnn_2_in=mmm_24_in + UID;
 nnn_3_in=StringLen(IntegerToString(nnn_2_in,0,32)); 
 nnn_4_in=nnn_2_in + int(MathPow(10.0,nnn_3_in));
 nnn_5_in=nnn_2_in + int(MathPow(10.0,nnn_3_in)) * 2;
 if ( !(mmm_29_bo) )
 {
   for (nnn_6_in = 0 ; nnn_6_in < 2 ; nnn_6_in ++)
   {
     nnn_7_in = 0 ;
     if ( CFAE::OrdersTotal() <= 0 )   continue;
     
     for ( ; nnn_7_in < CFAE::OrdersTotal() ; nnn_7_in ++)
     {
       if ( CFAE::OrderSelect(nnn_7_in,0,0) )
       {
         nnn_8_in = CFAE::OrderTicket() ;
         nnn_9_in = CFAE::OrderType() ;
         nnn_10_st = CFAE::OrderSymbol() ;
         nnn_11_do = CFAE::OrderLots() ;
         nnn_12_in = CFAE::OrderMagicNumber() ;
         nnn_13_do = CFAE::OrderTakeProfit() ;
         nnn_14_do = CFAE::OrderStopLoss() ;
         nnn_15_do = CFAE::OrderOpenTime() ;
         nnn_16_do = CFAE::OrderOpenPrice() ;
         ppp_do_1 = 0.0;
         if ( CFAE::MarketInfo(nnn_1_st,16) * nnn_11_do>mmm_25_do )
         {
           ppp_in_2 = CFAE::MarketInfo(nnn_1_st,12);
           ppp_do_3 = (CFAE::OrderCommission() + CFAE::OrderSwap()) / (CFAE::MarketInfo(nnn_1_st,16) * nnn_11_do);
           if ( CFAE::MarketInfo(nnn_1_st,11)>mmm_25_do )
           {
             ppp_do_4 = CFAE::MarketInfo(nnn_1_st,11);
           }
           else
           {
             ppp_do_4 = 0.00001;
           }
           ppp_do_3 = ppp_do_3 * ppp_do_4;
           ppp_do_1 = NormalizeDouble(ppp_do_3,ppp_in_2);
         }
         nnn_17_do = ppp_do_1 ;
         if ( nnn_6_in == 0 && nnn_9_in == 0 && nnn_10_st == nnn_1_st && nnn_12_in / 100 == nnn_4_in )
         {
           lizong_38(uuu_0_in,nnn_8_in,nnn_9_in,nnn_10_st,nnn_11_do,nnn_12_in,nnn_13_do,nnn_14_do,nnn_15_do,nnn_16_do,nnn_17_do); 
         }
         if ( nnn_6_in == 1 && nnn_9_in == 1 && nnn_10_st == nnn_1_st && nnn_12_in / 100 == nnn_5_in )
         {
           lizong_39(uuu_0_in,nnn_8_in,nnn_9_in,nnn_10_st,nnn_11_do,nnn_12_in,nnn_13_do,nnn_14_do,nnn_15_do,nnn_16_do,nnn_17_do); 
         }
       }
       else
       {
         Print(TradeComment + " " + nnn_1_st,": Failed to select an order! Error=",lizong_11(CFAE::GetLastError())); 
       }
     }
     
   }
 }
 }
//lizong_25 <<==--------   --------
 void lizong_26( int uuu_0_in)
 {
  string    nnn_1_st;
  int       nnn_2_in;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  int       nnn_6_in;
  int       nnn_7_in;
  int       nnn_8_in;
  int       nnn_9_in;
  int       nnn_10_in;
  int       nnn_11_in;
  string    nnn_12_st;
  double    nnn_13_do;
  int       nnn_14_in;
  double    nnn_15_do;
  double    nnn_16_do;
  long      nnn_17_lo;
  double    nnn_18_do;
  bool      nnn_19_bo;
  bool      nnn_20_bo;
//----- -----

 if ( CFAE::OrdersTotal() == 0 )   return;
 nnn_1_st = gainkit[uuu_0_in].st_1 ;
 nnn_2_in=mmm_24_in + UID;
 nnn_3_in=StringLen(IntegerToString(nnn_2_in,0,32)); 
 nnn_4_in=nnn_2_in + int(MathPow(10.0,nnn_3_in));
 nnn_5_in=nnn_2_in + int(MathPow(10.0,nnn_3_in)) * 2;
 nnn_6_in = CFAE::OrdersTotal() ;
 if ( nnn_6_in >  99 )
 {
   nnn_6_in = 99 ;
 }
 for (nnn_7_in = 0 ; nnn_7_in < 2 ; nnn_7_in ++)
 {
   nnn_8_in = 0 ;
   if ( nnn_6_in <= 0 )   continue;
   
   for ( ; nnn_8_in < nnn_6_in ; nnn_8_in ++)
   {
     nnn_9_in = 0 ;
     if ( CFAE::OrdersTotal() <= 0 )   continue;
     
     for ( ; nnn_9_in < CFAE::OrdersTotal() ; nnn_9_in ++)
     {
       if ( CFAE::OrderSelect(nnn_9_in,0,0) )
       {
         nnn_10_in = CFAE::OrderTicket() ;
         nnn_11_in = CFAE::OrderType() ;
         nnn_12_st = CFAE::OrderSymbol() ;
         nnn_13_do = CFAE::OrderLots() ;
         nnn_14_in = CFAE::OrderMagicNumber() ;
         nnn_15_do = CFAE::OrderTakeProfit() ;
         nnn_16_do = CFAE::OrderStopLoss() ;
         nnn_17_lo = CFAE::OrderOpenTime() ;
         nnn_18_do = CFAE::OrderOpenPrice() ;
         if ( nnn_7_in == 0 && nnn_11_in == 0 && nnn_12_st == nnn_1_st && nnn_14_in / 100 == nnn_4_in )
         {
           nnn_19_bo = lizong_44(uuu_0_in,nnn_10_in,nnn_11_in,nnn_12_st,nnn_13_do,nnn_14_in,nnn_15_do,nnn_16_do,nnn_17_lo,nnn_18_do) ;
           if ( nnn_19_bo )
           {
             break;
           }
         }
         if ( nnn_7_in == 1 && nnn_11_in == 1 && nnn_12_st == nnn_1_st && nnn_14_in / 100 == nnn_5_in )
         {
           nnn_20_bo = lizong_45(uuu_0_in,nnn_10_in,nnn_11_in,nnn_12_st,nnn_13_do,nnn_14_in,nnn_15_do,nnn_16_do,nnn_17_lo,nnn_18_do) ;
           if ( nnn_20_bo )
           {
             break;
           }
         }
       }
       else
       {
         Print(TradeComment + " " + nnn_1_st,": Failed to select an order! Error=",lizong_11(CFAE::GetLastError())); 
       }
     }
     
   }
   
 }
 }
//lizong_26 <<==--------   --------
 void lizong_27()
 {
  double    nnn_1_do_ko[];
  int       nnn_2_in;
  int       nnn_3_in;
//----- -----

 ArrayResize(nnn_1_do_ko,mmm_12_in,0); 
 ArrayFill(nnn_1_do_ko,0,mmm_12_in,0.0);
 nnn_2_in = -1 ;
 mmm_19_in = -1 ;
 if ( SmartTP )
 {
   nnn_2_in=-1 + 1;
   nnn_1_do_ko[nnn_2_in] = 58775.01158022;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 3854.012011184;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 39358.01174733;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 1269.011355758;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 56140.01164918;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 64530.01196917;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 60307.01246761;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 6648.014426477;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 45131.01330754;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 7950.01201108;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 45131.01330601;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 60854.01428551;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 65055.01297945;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 9460.013983523;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 10540.01337538;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 4544.014977765;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 248.0143470455;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 61247.0136825;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 52086.0134722;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 63574.01398307;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 47413.01467299;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 4155.014336146;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 2704.015830312;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 9089.014985123;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 45154.01433637;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 216.014348892;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 22495.01993742;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 9381.020399422;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 60747.01945847;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 65444.01670228;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 65217.01617163;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 64233.01657642;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 48506.01584509;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 33278.01883977;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 8650.017266761;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 48737.01661989;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 35446.0173142;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 55737.01834805;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 22494.01992731;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 15784.01696432;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 63403.01613634;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 42600.01646525;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 36063.01684867;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 41629.01739422;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 62737.01369688;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 45131.01330601;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 39673.0184521;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 48616.01696441;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 22822.01496536;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 9429.011354072;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 4667.014336799;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 2659.013857216;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 885.0113855871;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 60747.01481364;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 63709.01464703;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 9883.012018778;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 65481.01889697;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 6652.014425881;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 45131.01330867;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 1016.014955805;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 9460.013983523;
   nnn_2_in ++;
   nnn_1_do_ko[nnn_2_in] = 8284.018428598;
 }
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 57309.01392841;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 13471.01393551;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62737.01369688;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65243.01422747;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 18653.01429452;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 12883.01589119;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 17668.0156589;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61870.01519367;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 26663.01437642;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 22666.01491749;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 11113.01466572;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61047.01463275;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 5163.014844659;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 44787.01421445;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 40165.01459569;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 23094.01496487;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2643.015406373;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 5197.014638163;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4109.014394233;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 5323.01428411;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64308.01410924;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1851.013989072;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 25753.01453975;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 39664.01845956;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60744.01959539;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2651.020666013;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 29873.01918727;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64156.01948546;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 7404.017344148;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 56105.01633881;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64950.01613449;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 53211.01670127;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60156.01615407;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 40079.01584289;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64857.01557208;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 547.0162711932;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64866.01602218;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 7149.016702509;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64370.01570261;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10444.01640047;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 57251.01603322;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63101.01634664;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2348.016326638;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 57251.01603322;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6310.011802273;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 47990.01192367;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 8555.011328002;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 7442.011792083;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 19612.01145358;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1697.011001875;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 43477.0108115;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 46429.01090545;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60377.01181679;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3726.012653958;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 837.0122232008;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 5164.012393892;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6717.012155909;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 59263.01198725;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16432.01451182;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63387.01420649;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 13229.01392075;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 23889.01351881;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 928.0142407292;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3031.013743902;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2221.013470928;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 52513.01329229;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 36565.01402667;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 910.0137729072;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2770.013600246;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3064.013876089;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1755.013118797;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63219.01358184;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3441.013430833;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61433.01289695;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3852.013463712;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1755.012100862;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 20622.01368159;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3852.013463712;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4264.013583712;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4264.013583712;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 21333.01387241;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62934.01251469;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 56687.01271473;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 54267.01328379;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65375.01365708;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 31095.01427242;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64255.01373438;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48058.01300547;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61428.012654;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 35181.01479144;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63643.0154672;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 45936.01556469;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10320.01551479;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62218.01447119;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 44139.01458713;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 22822.01496536;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 5196.014638125;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 5315.014284631;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 627.0141667045;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2329.013082898;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 574.0145977273;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65391.01476261;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 35427.01384144;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 26273.01415376;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60782.01794053;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 12492.0194133;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2452.019703333;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 59819.01618939;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61780.01628349;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65105.01662631;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61390.01535454;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60092.01615633;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64793.01557475;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 422.0161619697;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62818.01602322;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 7085.016703258;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48490.0159386;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 38570.01618589;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9422.016099063;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65333.01563527;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4696.016474811;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64793.01602974;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62589.01635285;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65034.01592282;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61363.01583589;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64330.01020252;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2433.012330341;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2221.012248845;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 58964.01254474;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 49014.01192558;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63925.00960272;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 15798.01179155;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 11048.01204053;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 17565.01145348;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1700.011005076;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4447.011557045;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 797.0113839205;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1606.012653826;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 17092.01240473;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 27297.01221147;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63359.01199056;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61811.01297195;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16416.01451531;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65435.01421039;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 23897.01352519;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2976.014242831;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2951.013743267;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 52183.01402705;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60051.01456152;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 54130.01405045;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 399.0137739015;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 722.013601553;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 20910.01368195;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63218.01358308;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 11571.01343113;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63300.0130937;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 12456.01358552;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 56265.01031179;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6840.012158352;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 26272.01298145;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3406.013386619;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 12765.0118572;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9397.011358523;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64420.00960795;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 53460.00980464;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 27809.01180436;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4999.011699432;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9545.010567519;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61341.01175994;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 41941.01081364;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 11418.01181061;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48975.01144347;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4479.011554545;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 8989.011381345;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60369.01182045;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3276.012656042;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 17221.01222742;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63351.01198748;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65152.0135328;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3630.013954687;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1856.014249953;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3015.01374572;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 36567.01402781;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16981.01390998;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1747.013121383;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 735.0121057197;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 17268.01222799;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6292.0123616;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61421.0130191;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 21032.01438019;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63201.01366268;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3015.01374572;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16647.01573295;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 635.0138940341;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 55002.0122268;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62254.01501761;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 12947.01589384;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 59321.01548826;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 5190.016007273;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10576.01551276;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62862.01519499;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 12546.01440332;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48082.01486509;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 26809.01506428;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62219.01446873;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61171.01421608;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6718.014964422;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64268.01411022;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61046.01463234;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 54985.01946629;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3931.020664489;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 13479.02039716;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61290.01945805;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9361.01924536;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 13062.01894559;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65014.01613473;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 55213.01693375;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 388.0161624527;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 690.0163215909;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64874.01602347;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 12741.01614296;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61908.01628101;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62322.01405152;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 398.0137752178;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2258.013603097;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3379.013433182;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48657.01311622;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6198.014966373;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 13.01439551136;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64292.01411114;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 54763.01601634;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 38826.01618771;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65247.0142268;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 13011.0158911;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 27943.01549838;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61606.01519364;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 40101.01459483;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6206.014965862;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 77.0143927178;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2073.013081402;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6175.018758428;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3907.020667027;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 36315.01670303;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48234.01593876;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10445.01640248;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64795.01602865;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 52184.01182288;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2629.012066146;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1639.012648759;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 836.0122299432;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 17204.01223163;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65397.01199134;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65179.01420997;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 56609.01329214;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 35543.01402632;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62099.01456007;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 20654.01368307;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60866.01366031;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 11563.01343161;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 58775.01557738;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2851.016005265;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10490.01571146;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 13750.0154139;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61819.01297205;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62861.01423976;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 210.0161590246;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 22575.01496553;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64324.01410996;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 771.0186513258;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 12906.01467613;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1349.015917727;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 22067.01929612;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9351.019477102;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 13066.01894816;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 11557.01668195;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 18841.01608823;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 44426.01495178;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61331.01583266;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6182.014966477;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16725.01387396;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10701.01640389;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9416.016098703;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 11416.01181476;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 13477.02039932;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4872.019235492;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 45513.01928348;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6183.019680473;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 17522.01911291;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 14544.01618753;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 35541.01402647;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62780.01397489;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16910.01364792;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16613.0133896;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 49005.01608724;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1119.015516392;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 21264.01508722;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63343.01488099;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64992.01434217;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10842.01523296;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9519.015378333;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 21543.01564866;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64909.01513704;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 51170.01467243;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4892.01449553;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63321.01395811;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 54416.01475575;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 11645.0146381;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64255.01373438;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10465.0144106;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 8294.016047983;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62188.01252236;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 19305.01669887;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 50555.01332981;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1128.016370417;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 56942.01639359;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 25840.01660438;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6155.017036544;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 40009.01393721;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 53871.01700154;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9355.017067311;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 40156.01663305;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 44767.01293335;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9996.016453002;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 51550.01326464;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65000.01434072;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 56059.01323903;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 23541.01701494;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64425.01570618;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9304.014352055;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6917.014490909;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61862.01630003;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63481.01486609;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61360.01644927;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 58873.01664922;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64614.01347494;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63437.01270191;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 45037.01301862;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 8657.013331013;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63563.01602347;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48490.01584416;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 54448.01475665;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2273.014411288;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3807.012108958;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 53682.01457561;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4626.013807017;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62712.01463289;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9515.015378485;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1688.016103854;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9376.014633722;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 17005.01676512;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 51174.01467303;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10903.01650006;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16649.01689754;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4557.016143011;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1087.016112169;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60666.01589207;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 7780.014078191;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1826.016364498;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 55286.01308316;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60318.01598253;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 409.0126363542;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62493.01262849;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3144.012697102;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 816.01689375;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6189.016596307;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61171.01421328;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 18840.01609098;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 56717.0151377;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48873.01657642;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 3657.013662689;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 38314.01618546;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1916.013339555;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 390.0144965246;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 51703.01271346;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63313.01395756;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 5980.013519356;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 14188.01642238;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62902.01596231;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63428.01309241;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 60381.01738902;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48477.01091287;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 56795.01954348;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 35423.01605786;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65441.01669926;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 6901.017011866;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 36605.01596594;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61870.01629715;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 57185.01644852;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63764.01661937;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64630.01347598;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61238.01651973;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16715.01689844;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61338.01270005;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48118.01323105;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1079.016112992;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 59326.01560837;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 11579.01343258;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64466.01269705;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61639.01602384;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 55294.01308541;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4956.013521297;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 48474.01584589;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10540.01633083;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 12984.01358776;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 54955.01318312;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 11563.01343161;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 43477.0108115;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 192.0185782197;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64810.01608257;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 13419.01558728;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 65221.01616853;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64519.0164206;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64300.0141106;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 51120.0159382;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 1122.013547756;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16482.01354835;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4616.012207945;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 39673.0184521;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 61151.01293346;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 58280.01336552;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 51839.01606055;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 54130.01405045;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 22491.01541652;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 526.0136482102;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2258.0134966;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16806.01208334;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 4520.010874953;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 16482.0191152;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 9883.012018778;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 7950.01201108;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 2442.013018684;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 17506.01354839;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 18713.01308448;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 785.0162674716;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64858.01196998;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63817.01605056;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 62899.01609798;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 690.0163181061;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 7084.016704384;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 63966.01331726;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 25298.01419737;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 64332.01410942;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 7736.013030312;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 5635.013818911;
 nnn_2_in ++;
 nnn_1_do_ko[nnn_2_in] = 10340.01359628;
 nnn_2_in ++;
 for (nnn_3_in = 0 ; nnn_3_in < nnn_2_in ; nnn_3_in ++)
 {
   mmm_19_in ++;
   mmm_17_lo_ko[mmm_19_in] = int(nnn_1_do_ko[nnn_3_in]);
   mmm_18_do_ko[mmm_19_in] = (int(nnn_1_do_ko[nnn_3_in]) - int(nnn_1_do_ko[nnn_3_in])) * 66.0;
 }
 }
//lizong_27 <<==--------   --------
 void lizong_28( int uuu_0_in)
 {
  string    nnn_1_st;
  int       nnn_2_in;
  int       nnn_3_in;
  int       nnn_4_in;
  double    nnn_5_do;
  double    nnn_6_do;
  string    nnn_7_st;
  int       nnn_8_in;
  double    nnn_9_do;
  double    nnn_10_do;
  int       nnn_11_in;
  int       nnn_12_in;
  double    nnn_13_do;
//----- -----
 string     ppp_st_1;
 double     ppp_do_2;
 int        ppp_in_3;
 long       ppp_lo_4;
 double     ppp_do_5;

 nnn_1_st = gainkit[uuu_0_in].st_1 ;
 nnn_2_in = 1 ;
 if ( gainkit[uuu_0_in].bo_18 != 0x0 )
 {
   nnn_2_in = 96 ;
 }
 for (nnn_3_in = 0 ; nnn_3_in < nnn_2_in ; nnn_3_in ++)
 {
   nnn_4_in = 16 ;
   nnn_5_do = 0.002 ;
   nnn_6_do = 0.0 ;
   nnn_7_st = "" ;
   gainkit[uuu_0_in].lo_16 = 0;
   gainkit[uuu_0_in].do_17 = 0.0;
   if ( CFAE::iBars(nnn_1_st,mmm_21_in) <  nnn_4_in * 2 + nnn_3_in )
   {
     return;
   }
   for (nnn_8_in = 1 ; nnn_8_in <= nnn_4_in ; nnn_8_in ++)
   {
     nnn_9_do = CFAE::iClose(nnn_1_st,mmm_21_in,nnn_8_in + nnn_3_in) ;
     nnn_10_do = CFAE::iOpen(nnn_1_st,mmm_21_in,nnn_8_in + nnn_3_in) ;
     nnn_6_do = nnn_6_do + nnn_9_do ;
     if ( nnn_9_do - nnn_10_do>=0.0 )
     {
       nnn_7_st +="1";
     }
     else
     {
       nnn_7_st +="0";
     }
   }
   gainkit[uuu_0_in].do_17 = nnn_6_do / nnn_4_in;
   ppp_st_1 = nnn_7_st;
   ppp_do_2 = 0.0;
   for (ppp_in_3 = 0 ; ppp_in_3 < StringLen(ppp_st_1)  ; ppp_in_3=ppp_in_3 + 1)
   {
     if ( StringGetCharacter(ppp_st_1,ppp_in_3) == 49 )
     {
       ppp_lo_4=ppp_do_2 * 2 + 1;
     }
   }
   gainkit[uuu_0_in].lo_16 = ppp_lo_4;
   if ( gainkit[uuu_0_in].bo_5 == 0x0 && gainkit[uuu_0_in].bo_6 == 0x0 && gainkit[uuu_0_in].bo_19 == 0x0 && gainkit[uuu_0_in].bo_20 == 0x0 )
   {
     return;
   }
   for (nnn_11_in=mmm_12_in / 100 - 1 ; nnn_11_in >= 0 ; nnn_11_in --)
   {
     nnn_12_in=(nnn_11_in + 1) * 100 - 1;
     if ( nnn_12_in < nnn_11_in * 100 )   continue;
     
     for ( ; nnn_12_in >= nnn_11_in * 100 ; nnn_12_in --)
     {
       if ( mmm_18_do_ko[nnn_12_in]<mmm_25_do )   break;
       
       if ( gainkit[uuu_0_in].do_17<mmm_18_do_ko[nnn_11_in * 100] )   break;
       nnn_13_do = 1.0 ;
       if ( mmm_18_do_ko[nnn_12_in]<0.0 )
       {
         nnn_13_do = -1.0 ;
       }
       ppp_do_5 = nnn_5_do * nnn_13_do;
       if ( !(gainkit[uuu_0_in].do_17<(nnn_5_do * nnn_13_do + 1.0) * mmm_18_do_ko[nnn_12_in]) || !(gainkit[uuu_0_in].do_17>(1.0 - ppp_do_5) * mmm_18_do_ko[nnn_12_in]) || gainkit[uuu_0_in].lo_16 != mmm_17_lo_ko[nnn_12_in] )   continue;
       gainkit[uuu_0_in].bo_5 = false;
       gainkit[uuu_0_in].bo_6 = false;
       gainkit[uuu_0_in].bo_19 = false;
       gainkit[uuu_0_in].bo_20 = false;
       break;
       
     }
     
   }
 }
 gainkit[uuu_0_in].bo_18 = false;
 }
//lizong_28 <<==--------   --------
 void lizong_29()
 {
  double    nnn_1_do = 0.0;
  double    nnn_2_do;
//----- -----
 double     ppp_do_1;
 int        ppp_in_2;
 int        ppp_in_3;
 int        ppp_in_4;
 int        ppp_in_5;
 string     ppp_st_6;
 int        ppp_in_7;
 int        ppp_in_8;
 int        ppp_in_9;
 int        ppp_in_10;
 int        ppp_in_11;
 double     ppp_do_12;
 int        ppp_in_13;
 int        ppp_in_14;
 int        ppp_in_15;
 int        ppp_in_16;
 string     ppp_st_17;
 int        ppp_in_18;
 int        ppp_in_19;
 int        ppp_in_20;
 int        ppp_in_21;
 int        ppp_in_22;

 if ( MaximumDrawdown>mmm_25_do && MaximumDrawdown<99.99 )
 {
   if ( DrawdownCalculation == 1 )
   {
     ppp_do_1 = 0.0;
     ppp_in_2 = mmm_24_in + UID + int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32)) ));
     ppp_in_3 = mmm_24_in + UID + int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32)) )) * 2;
     for (ppp_in_4 = 0 ; ppp_in_4 < CFAE::OrdersTotal() ; ppp_in_4=ppp_in_4 + 1)
     {
       if ( CFAE::OrderSelect(ppp_in_4,0,0) )
       {
         ppp_in_5 = CFAE::OrderType();
         CFAE::OrderSymbol(); 
         ppp_in_7 = CFAE::OrderMagicNumber() / 100;
         if ( ( ( ppp_in_5 != 0 || ppp_in_2 != ppp_in_7 ) && (ppp_in_5 != 1 || ppp_in_3 != ppp_in_7) ) )   continue;
         ppp_do_1 = CFAE::OrderProfit() + CFAE::OrderSwap() + CFAE::OrderCommission() + ppp_do_1;
          continue;
       }
       Print(TradeComment + " " + "------",": Failed to select an order! Error=",lizong_11(CFAE::GetLastError())); 
       
     }
     nnn_1_do = -(ppp_do_1);
   }
   if ( DrawdownCalculation == 0 )
   {
     nnn_1_do = AccountInfoDouble(ACCOUNT_BALANCE) - AccountInfoDouble(ACCOUNT_EQUITY) ;
   }
   if ( nnn_1_do>MaximumDrawdown / 100.0 * AccountInfoDouble(ACCOUNT_BALANCE) )
   {
     if ( MaximumDrawdownAction == 0 )
     {
       mmm_29_bo = true ;
       mmm_30_in = 24 ;
       for (ppp_in_8 = 0 ; ppp_in_8 < ArraySize(gainkit) ; ppp_in_8=ppp_in_8 + 1)
       {
         gainkit[ppp_in_8].bo_5 = false;
         gainkit[ppp_in_8].bo_6 = false;
       }
     }
     if ( MaximumDrawdownAction == 1 )
     {
       mmm_29_bo = true ;
       mmm_31_bo = true ;
       for (ppp_in_9 = 0 ; ppp_in_9 < ArraySize(gainkit) ; ppp_in_9=ppp_in_9 + 1)
       {
         gainkit[ppp_in_9].bo_5 = false;
         gainkit[ppp_in_9].bo_6 = false;
       }
     }
     if ( MaximumDrawdownAction == 2 )
     {
       for (ppp_in_10 = 0 ; ppp_in_10 < ArraySize(gainkit) ; ppp_in_10=ppp_in_10 + 1)
       {
         gainkit[ppp_in_10].bo_5 = false;
         gainkit[ppp_in_10].bo_6 = false;
       }
     }
     if ( MaximumDrawdownAction == 3 )
     {
       mmm_31_bo = true ;
       for (ppp_in_11 = 0 ; ppp_in_11 < ArraySize(gainkit) ; ppp_in_11=ppp_in_11 + 1)
       {
         gainkit[ppp_in_11].bo_5 = false;
         gainkit[ppp_in_11].bo_6 = false;
       }
     }
   }
 }
 if ( !(MaximumDrawdownMoney>mmm_25_do) )   return;
 nnn_2_do = 0.0 ;
 if ( DrawdownCalculation == 1 )
 {
   ppp_do_12 = 0.0;
   ppp_in_13 = mmm_24_in + UID + int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32)) ));
   ppp_in_14 = mmm_24_in + UID + int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32)) )) * 2;
   for (ppp_in_15 = 0 ; ppp_in_15 < CFAE::OrdersTotal() ; ppp_in_15=ppp_in_15 + 1)
   {
     if ( CFAE::OrderSelect(ppp_in_15,0,0) )
     {
       ppp_in_16 = CFAE::OrderType();
       CFAE::OrderSymbol(); 
       ppp_in_18 = CFAE::OrderMagicNumber() / 100;
       if ( ( ( ppp_in_16 != 0 || ppp_in_13 != ppp_in_18 ) && (ppp_in_16 != 1 || ppp_in_14 != ppp_in_18) ) )   continue;
       ppp_do_12 = CFAE::OrderProfit() + CFAE::OrderSwap() + CFAE::OrderCommission() + ppp_do_12;
        continue;
     }
     Print(TradeComment + " " + "------",": Failed to select an order! Error=",lizong_11(CFAE::GetLastError())); 
     
   }
   nnn_2_do = -(ppp_do_12);
 }
 if ( DrawdownCalculation == 0 )
 {
   nnn_2_do = AccountInfoDouble(ACCOUNT_BALANCE) - AccountInfoDouble(ACCOUNT_EQUITY) ;
 }
 if ( !(nnn_2_do>MaximumDrawdownMoney) )   return;
 
 if ( MaximumDrawdownAction == 0 )
 {
   mmm_29_bo = true ;
   mmm_30_in = 24 ;
   for (ppp_in_19 = 0 ; ppp_in_19 < ArraySize(gainkit) ; ppp_in_19=ppp_in_19 + 1)
   {
     gainkit[ppp_in_19].bo_5 = false;
     gainkit[ppp_in_19].bo_6 = false;
   }
 }
 if ( MaximumDrawdownAction == 1 )
 {
   mmm_29_bo = true ;
   mmm_31_bo = true ;
   for (ppp_in_20 = 0 ; ppp_in_20 < ArraySize(gainkit) ; ppp_in_20=ppp_in_20 + 1)
   {
     gainkit[ppp_in_20].bo_5 = false;
     gainkit[ppp_in_20].bo_6 = false;
   }
 }
 if ( MaximumDrawdownAction == 2 )
 {
   for (ppp_in_21 = 0 ; ppp_in_21 < ArraySize(gainkit) ; ppp_in_21=ppp_in_21 + 1)
   {
     gainkit[ppp_in_21].bo_5 = false;
     gainkit[ppp_in_21].bo_6 = false;
   }
 }
 if ( MaximumDrawdownAction != 3 )   return;
 mmm_31_bo = true ;
 for (ppp_in_22 = 0 ; ppp_in_22 < ArraySize(gainkit) ; ppp_in_22=ppp_in_22 + 1)
 {
   gainkit[ppp_in_22].bo_5 = false;
   gainkit[ppp_in_22].bo_6 = false;
 }
 }
//lizong_29 <<==--------   --------
 bool lizong_30( string uuu_0_st,int uuu_1_in,int uuu_2_in,double uuu_3_do,double uuu_4_do,double uuu_5_do,double uuu_6_do,double uuu_7_do,double uuu_8_do)
 {
  bool      nnn_1_bo;
  int       nnn_2_in;
  int       nnn_3_in;
  int       nnn_4_in;
  double    nnn_5_do;
  double    nnn_6_do;
  double    nnn_7_do;
  double    nnn_8_do;
  double    nnn_9_do;
  double    nnn_10_do;
  double    nnn_11_do;
  int       nnn_12_in;
  double    nnn_13_do;
  double    nnn_14_do;
//----- -----

 if ( mmm_5_in == 0 )
 {
   return(false); 
 }
 if ( mmm_28_in == 0 && CFAE::TimeMinute(TimeCurrent()) <= 1 && !(CFAE::IsTesting()) )
 {
   return(false); 
 }
 if ( mmm_28_in == 0 && CFAE::TimeMinute(TimeCurrent()) <= 5 && CFAE::TimeDayOfWeek(mmm_28_in) == 1 && !(CFAE::IsTesting()) )
 {
   return(false); 
 }
 nnn_2_in = 0 ;
 nnn_3_in = -1 ;
 nnn_4_in = 0 ;
 nnn_5_do = 0.0 ;
 nnn_6_do = 0.0 ;
 nnn_7_do = 0.0 ;
 nnn_8_do = 0.0 ;
 nnn_9_do = 0.0 ;
 nnn_10_do = 0.0 ;
 nnn_11_do = CFAE::MarketInfo(uuu_0_st,11) ;
 nnn_12_in = CFAE::MarketInfo(uuu_0_st,12) ;
 nnn_13_do = NormalizeDouble(CFAE::MarketInfo(uuu_0_st,14) * nnn_11_do,nnn_12_in) ;
 nnn_14_do = NormalizeDouble(CFAE::MarketInfo(uuu_0_st,33) * nnn_11_do,nnn_12_in) ;
 nnn_2_in = uuu_1_in ;
 nnn_3_in = uuu_2_in ;
 nnn_4_in=uuu_1_in * 10 + uuu_2_in;
 if ( uuu_1_in == 1 )
 {
   nnn_5_do = NormalizeDouble(uuu_3_do,nnn_12_in) ;
   nnn_6_do = NormalizeDouble(uuu_5_do,nnn_12_in) ;
   nnn_7_do = NormalizeDouble(uuu_4_do,nnn_12_in) ;
 }
 if ( nnn_2_in == 2 )
 {
   nnn_8_do = NormalizeDouble(uuu_6_do,nnn_12_in) ;
   nnn_9_do = NormalizeDouble(uuu_8_do,nnn_12_in) ;
   nnn_10_do = NormalizeDouble(uuu_7_do,nnn_12_in) ;
 }
 if ( nnn_2_in == 3 )
 {
   nnn_5_do = NormalizeDouble(uuu_3_do,nnn_12_in) ;
   nnn_6_do = NormalizeDouble(uuu_5_do,nnn_12_in) ;
   nnn_7_do = NormalizeDouble(uuu_4_do,nnn_12_in) ;
   nnn_8_do = NormalizeDouble(uuu_6_do,nnn_12_in) ;
   nnn_9_do = NormalizeDouble(uuu_8_do,nnn_12_in) ;
   nnn_10_do = NormalizeDouble(uuu_7_do,nnn_12_in) ;
 }
 CFAE::RefreshRates(); 
 switch(nnn_4_in)
 {
   case 10 :
   if ( ( !(NormalizeDouble(CFAE::MarketInfo(uuu_0_st,9) - nnn_7_do,nnn_12_in)>nnn_14_do) && !(nnn_7_do<nnn_11_do) ) || ( !(NormalizeDouble(nnn_6_do - CFAE::MarketInfo(uuu_0_st,9),nnn_12_in)>nnn_14_do) && !(nnn_6_do<nnn_11_do) ) || nnn_2_in != 1 )   break;
   return(true); 
   case 11 :
   if ( ( !(NormalizeDouble(nnn_7_do - CFAE::MarketInfo(uuu_0_st,10),nnn_12_in)>nnn_14_do) && !(nnn_7_do<nnn_11_do) ) || ( !(NormalizeDouble(CFAE::MarketInfo(uuu_0_st,10) - nnn_6_do,nnn_12_in)>nnn_14_do) && !(nnn_6_do<nnn_11_do) ) || nnn_2_in != 1 )   break;
   return(true); 
   case 12 :
   if ( !(NormalizeDouble(CFAE::MarketInfo(uuu_0_st,10) - nnn_5_do,nnn_12_in)>nnn_14_do) || ( !(nnn_13_do<NormalizeDouble(nnn_5_do - nnn_7_do,nnn_12_in)) && !(nnn_7_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_6_do - nnn_5_do,nnn_12_in)) && !(nnn_6_do<nnn_11_do) ) || nnn_2_in != 1 )   break;
   return(true); 
   case 13 :
   if ( !(NormalizeDouble(nnn_5_do - CFAE::MarketInfo(uuu_0_st,9),nnn_12_in)>nnn_14_do) || ( !(nnn_13_do<NormalizeDouble(nnn_7_do - nnn_5_do,nnn_12_in)) && !(nnn_7_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_5_do - nnn_6_do,nnn_12_in)) && !(nnn_6_do<nnn_11_do) ) || nnn_2_in != 1 )   break;
   return(true); 
   case 14 :
   if ( !(NormalizeDouble(nnn_5_do - CFAE::MarketInfo(uuu_0_st,10),nnn_12_in)>nnn_14_do) || ( !(nnn_13_do<NormalizeDouble(nnn_5_do - nnn_7_do,nnn_12_in)) && !(nnn_7_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_6_do - nnn_5_do,nnn_12_in)) && !(nnn_6_do<nnn_11_do) ) || nnn_2_in != 1 )   break;
   return(true); 
   case 15 :
   if ( !(NormalizeDouble(CFAE::MarketInfo(uuu_0_st,9) - nnn_5_do,nnn_12_in)>nnn_14_do) || ( !(nnn_13_do<NormalizeDouble(nnn_7_do - nnn_5_do,nnn_12_in)) && !(nnn_7_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_5_do - nnn_6_do,nnn_12_in)) && !(nnn_6_do<nnn_11_do) ) || nnn_2_in != 1 )   break;
   return(true); 
   case 20 :
   if ( ( !(nnn_13_do<NormalizeDouble(CFAE::MarketInfo(uuu_0_st,9) - nnn_10_do,nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_9_do - CFAE::MarketInfo(uuu_0_st,9),nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) )   break;
   return(true); 
   case 21 :
   if ( ( !(nnn_13_do<NormalizeDouble(nnn_10_do - CFAE::MarketInfo(uuu_0_st,10),nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(CFAE::MarketInfo(uuu_0_st,10) - nnn_9_do,nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) )   break;
   return(true); 
   case 22 :
   if ( !(nnn_13_do<NormalizeDouble(CFAE::MarketInfo(uuu_0_st,10) - nnn_8_do,nnn_12_in)) || ( !(nnn_13_do<NormalizeDouble(nnn_8_do - nnn_10_do,nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_9_do - nnn_8_do,nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) || nnn_2_in != 2 )   break;
   return(true); 
   case 23 :
   if ( !(nnn_13_do<NormalizeDouble(nnn_8_do - CFAE::MarketInfo(uuu_0_st,9),nnn_12_in)) || ( !(nnn_13_do<NormalizeDouble(nnn_10_do - nnn_8_do,nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_8_do - nnn_9_do,nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) || nnn_2_in != 2 )   break;
   return(true); 
   case 24 :
   if ( !(nnn_13_do<NormalizeDouble(nnn_8_do - CFAE::MarketInfo(uuu_0_st,10),nnn_12_in)) || ( !(nnn_13_do<NormalizeDouble(nnn_8_do - nnn_10_do,nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_9_do - nnn_8_do,nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) || nnn_2_in != 2 )   break;
   return(true); 
   case 25 :
   if ( !(nnn_13_do<NormalizeDouble(CFAE::MarketInfo(uuu_0_st,9) - nnn_8_do,nnn_12_in)) || ( !(nnn_13_do<NormalizeDouble(nnn_10_do - nnn_8_do,nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_8_do - nnn_9_do,nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) || nnn_2_in != 2 )   break;
   return(true); 
   case 30 :
   if ( ( !(NormalizeDouble(CFAE::MarketInfo(uuu_0_st,9) - nnn_7_do,nnn_12_in)>nnn_14_do) && !(nnn_7_do<nnn_11_do) ) || ( !(NormalizeDouble(nnn_6_do - CFAE::MarketInfo(uuu_0_st,9),nnn_12_in)>nnn_14_do) && !(nnn_6_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(CFAE::MarketInfo(uuu_0_st,9) - nnn_10_do,nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_9_do - CFAE::MarketInfo(uuu_0_st,9),nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) )   break;
   return(true); 
   case 31 :
   if ( ( !(NormalizeDouble(nnn_7_do - CFAE::MarketInfo(uuu_0_st,10),nnn_12_in)>nnn_14_do) && !(nnn_7_do<nnn_11_do) ) || ( !(NormalizeDouble(CFAE::MarketInfo(uuu_0_st,10) - nnn_6_do,nnn_12_in)>nnn_14_do) && !(nnn_6_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_10_do - CFAE::MarketInfo(uuu_0_st,10),nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(CFAE::MarketInfo(uuu_0_st,10) - nnn_9_do,nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) )   break;
   return(true); 
   case 32 :
   if ( !(NormalizeDouble(CFAE::MarketInfo(uuu_0_st,10) - nnn_5_do,nnn_12_in)>nnn_14_do) || ( !(nnn_13_do<NormalizeDouble(nnn_5_do - nnn_7_do,nnn_12_in)) && !(nnn_7_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_6_do - nnn_5_do,nnn_12_in)) && !(nnn_6_do<nnn_11_do) ) || !(nnn_13_do<NormalizeDouble(CFAE::MarketInfo(uuu_0_st,10) - nnn_8_do,nnn_12_in)) || ( !(nnn_13_do<NormalizeDouble(nnn_8_do - nnn_10_do,nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_9_do - nnn_8_do,nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) )   break;
   return(true); 
   case 33 :
   if ( !(NormalizeDouble(nnn_5_do - CFAE::MarketInfo(uuu_0_st,9),nnn_12_in)>nnn_14_do) || ( !(nnn_13_do<NormalizeDouble(nnn_7_do - nnn_5_do,nnn_12_in)) && !(nnn_7_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_5_do - nnn_6_do,nnn_12_in)) && !(nnn_6_do<nnn_11_do) ) || !(nnn_13_do<NormalizeDouble(nnn_8_do - CFAE::MarketInfo(uuu_0_st,9),nnn_12_in)) || ( !(nnn_13_do<NormalizeDouble(nnn_10_do - nnn_8_do,nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_8_do - nnn_9_do,nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) )   break;
   return(true); 
   case 34 :
   if ( !(NormalizeDouble(nnn_5_do - CFAE::MarketInfo(uuu_0_st,10),nnn_12_in)>nnn_14_do) || ( !(nnn_13_do<NormalizeDouble(nnn_5_do - nnn_7_do,nnn_12_in)) && !(nnn_7_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_6_do - nnn_5_do,nnn_12_in)) && !(nnn_6_do<nnn_11_do) ) || !(nnn_13_do<NormalizeDouble(nnn_8_do - CFAE::MarketInfo(uuu_0_st,10),nnn_12_in)) || ( !(nnn_13_do<NormalizeDouble(nnn_8_do - nnn_10_do,nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_9_do - nnn_8_do,nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) )   break;
   return(true); 
   case 35 :
   if ( !(NormalizeDouble(CFAE::MarketInfo(uuu_0_st,9) - nnn_5_do,nnn_12_in)>nnn_14_do) || ( !(nnn_13_do<NormalizeDouble(nnn_7_do - nnn_5_do,nnn_12_in)) && !(nnn_7_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_5_do - nnn_6_do,nnn_12_in)) && !(nnn_6_do<nnn_11_do) ) || !(nnn_13_do<NormalizeDouble(CFAE::MarketInfo(uuu_0_st,9) - nnn_8_do,nnn_12_in)) || ( !(nnn_13_do<NormalizeDouble(nnn_10_do - nnn_8_do,nnn_12_in)) && !(nnn_10_do<nnn_11_do) ) || ( !(nnn_13_do<NormalizeDouble(nnn_8_do - nnn_9_do,nnn_12_in)) && !(nnn_9_do<nnn_11_do) ) )   break;
   return(true); 
 }
 return(false); 
 }
//lizong_30 <<==--------   --------
 void lizong_31( string uuu_0_st,int uuu_1_in,int uuu_2_in,int uuu_3_in,string uuu_4_st,string uuu_5_st,color uuu_6_co,int uuu_7_in)
 {
 if ( CFAE::ObjectFind(0,uuu_0_st) != -1 )
 {
   CFAE::ObjectSetText(uuu_0_st,uuu_4_st,uuu_7_in,uuu_5_st,uuu_6_co); 
   return;
 }
 if ( !(CFAE::ObjectCreate(uuu_0_st,23,uuu_1_in,0,0.0,0,0.0,0,0.0)) )   return;
 CFAE::ObjectSet(uuu_0_st,101,0.0); 
 CFAE::ObjectSet(uuu_0_st,1028,1.0); 
 CFAE::ObjectSet(uuu_0_st,1000,0.0); 
 CFAE::ObjectSetString(0,uuu_0_st,206,"WakaWakaEA"); 
 CFAE::ObjectSetInteger(0,uuu_0_st,OBJPROP_HIDDEN,1); 
 CFAE::ObjectSet(uuu_0_st,102,uuu_2_in); 
 CFAE::ObjectSet(uuu_0_st,103,uuu_3_in); 
 CFAE::ObjectSetText(uuu_0_st,uuu_4_st,uuu_7_in,uuu_5_st,uuu_6_co); 
 }
//lizong_31 <<==--------   --------
 void lizong_32( int uuu_0_in)
 {
  string    nnn_1_st;
  int       nnn_2_in;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  int       nnn_6_in;
  int       nnn_7_in;
  int       nnn_8_in;
  int       nnn_9_in;
  int       nnn_10_in;
  int       nnn_11_in;
  int       nnn_12_in;
  int       nnn_13_in;
  int       nnn_14_in;
  int       nnn_15_in;
  int       nnn_16_in;
  int       nnn_17_in;
  int       nnn_18_in;
  int       nnn_19_in;
  int       nnn_20_in;
  int       nnn_21_in;
  int       nnn_22_in;
  bool      nnn_23_bo;
  int       nnn_24_in;
  int       nnn_25_in;
  int       nnn_26_in;
  int       nnn_27_in;
  int       nnn_28_in;
  datetime  nnn_29_da;
  int       nnn_30_in;
  datetime  nnn_31_da;
  int       nnn_32_in;
  int       nnn_33_in;
  int       nnn_34_in;
  int       nnn_35_in;
  int       nnn_36_in;
  int       nnn_37_in;
  int       nnn_38_in;
  bool      nnn_39_bo;
  int       nnn_40_in;
  int       nnn_41_in;
  int       nnn_42_in;
  int       nnn_43_in;
  int       nnn_44_in;
  int       nnn_45_in;
  double    nnn_46_do;
  double    nnn_47_do;
  double    nnn_48_do;
  double    nnn_49_do;
  double    nnn_50_do;
  double    nnn_51_do;
  double    nnn_52_do;
  double    nnn_53_do;
  int       nnn_54_in;
//----- -----
 int        ppp_in_1;
 string     ppp_st_2;
 int        ppp_in_3;
 string     ppp_st_4;
 bool       ppp_bo_5;
 bool       ppp_bo_6;
 int        ppp_in_7;
 int        ppp_in_8;
 int        ppp_in_9;
 int        ppp_in_10;
 int        ppp_in_11;
 int        ppp_in_12;

 gainkit[uuu_0_in].in_4 ++;
 nnn_1_st = gainkit[uuu_0_in].st_1 ;
 nnn_2_in = 86400 ;
 nnn_3_in = 0 ;
 nnn_4_in = 1 ;
 nnn_5_in=1 + 1;
 nnn_6_in=nnn_5_in + 1;
 nnn_7_in=nnn_5_in + nnn_5_in;
 nnn_8_in=nnn_6_in + nnn_5_in;
 nnn_9_in=nnn_6_in + nnn_6_in;
 nnn_10_in=nnn_7_in + nnn_6_in;
 nnn_11_in=nnn_9_in + nnn_5_in;
 nnn_12_in=nnn_9_in + nnn_6_in;
 nnn_13_in = 0 ;
 nnn_14_in = 1 ;
 nnn_15_in = nnn_5_in ;
 nnn_16_in = nnn_6_in ;
 nnn_17_in=nnn_6_in + 1;
 nnn_18_in=nnn_7_in + 1;
 nnn_19_in=nnn_18_in + 1;
 nnn_20_in=nnn_5_in + nnn_18_in;
 nnn_21_in=nnn_17_in + nnn_17_in;
 nnn_22_in=nnn_21_in + 1;
 nnn_23_bo = true ;
 mmm_7_da = TimeCurrent() ;
 nnn_24_in = CFAE::TimeHour(mmm_7_da) ;
 nnn_25_in = CFAE::TimeMinute(mmm_7_da) ;
 nnn_26_in = MathFloor(nnn_25_in / 15.0) * 15.0 ;
 nnn_27_in = 0 ;
 nnn_28_in = 0 ;
 ResetLastError();
 nnn_29_da = CFAE::iTime(nnn_1_st,15,0) ;
 nnn_28_in = CFAE::GetLastError() ;
 if ( ( CFAE::TimeMinute(nnn_29_da) != nnn_26_in || nnn_28_in == 4066 ) && mmm_7_da >  0 )
 {
   for (nnn_30_in = 0 ; nnn_30_in < 10 ; nnn_30_in ++)
   {
     Sleep(1000); 
     ResetLastError();
     nnn_29_da = CFAE::iTime(nnn_1_st,15,0) ;
     nnn_27_in = CFAE::GetLastError() ;
     if ( nnn_27_in != 0 )   continue;
     if ( CFAE::TimeMinute(nnn_29_da) == nnn_26_in )   break;
     
   }
   if ( ( CFAE::TimeMinute(nnn_29_da) != nnn_26_in || nnn_27_in == 4066 ) && gainkit[uuu_0_in].in_4 >  0x1 && nnn_27_in >  0 )
   {
     ppp_in_1 = mmm_21_in;
     ppp_st_2 = "current";
     if ( mmm_21_in == 0 )
     {
       ppp_st_2 = "current";
     }
     if ( ppp_in_1 == 1 )
     {
       ppp_st_2 = "M1";
     }
     if ( ppp_in_1 == 5 )
     {
       ppp_st_2 = "M5";
     }
     if ( ppp_in_1 == 0xF )
     {
       ppp_st_2 = "M15";
     }
     if ( ppp_in_1 == 30 )
     {
       ppp_st_2 = "M30";
     }
     if ( ppp_in_1 == 60 )
     {
       ppp_st_2 = "H1";
     }
     if ( ppp_in_1 == 240 )
     {
       ppp_st_2 = "H4";
     }
     if ( ppp_in_1 == 1440 )
     {
       ppp_st_2 = "D1";
     }
     if ( ppp_in_1 == 10080 )
     {
       ppp_st_2 = "W1";
     }
     if ( ppp_in_1 == 43200 )
     {
       ppp_st_2 = "MN1";
     }
     Print(TradeComment + " " + nnn_1_st,":",lizong_11(nnn_27_in)," when updating history on ",ppp_st_2); 
     nnn_23_bo = false ;
   }
 }
 if ( CFAE::iBars(nnn_1_st,mmm_21_in) <  1000 )
 {
   ppp_in_3 = mmm_21_in;
   ppp_st_4 = "current";
   if ( mmm_21_in == 0 )
   {
     ppp_st_4 = "current";
   }
   if ( ppp_in_3 == 1 )
   {
     ppp_st_4 = "M1";
   }
   if ( ppp_in_3 == 5 )
   {
     ppp_st_4 = "M5";
   }
   if ( ppp_in_3 == 0xF )
   {
     ppp_st_4 = "M15";
   }
   if ( ppp_in_3 == 30 )
   {
     ppp_st_4 = "M30";
   }
   if ( ppp_in_3 == 60 )
   {
     ppp_st_4 = "H1";
   }
   if ( ppp_in_3 == 240 )
   {
     ppp_st_4 = "H4";
   }
   if ( ppp_in_3 == 1440 )
   {
     ppp_st_4 = "D1";
   }
   if ( ppp_in_3 == 10080 )
   {
     ppp_st_4 = "W1";
   }
   if ( ppp_in_3 == 43200 )
   {
     ppp_st_4 = "MN1";
   }
   Print(TradeComment + " " + nnn_1_st,": Not enough historical data on ",ppp_st_4); 
   nnn_23_bo = false ;
   nnn_3_in = 1 ;
   nnn_4_in = 1 ;
   nnn_5_in = 1 ;
   nnn_6_in = 1 ;
   nnn_7_in = 1 ;
   nnn_8_in = 1 ;
   nnn_9_in = 1 ;
   nnn_10_in = 1 ;
   nnn_11_in = 1 ;
   nnn_12_in = 1 ;
   nnn_13_in = 1 ;
   nnn_14_in = 1 ;
   nnn_15_in = 1 ;
   nnn_16_in = 1 ;
   nnn_17_in = 1 ;
   nnn_18_in = 1 ;
   nnn_19_in = 1 ;
   nnn_20_in = 1 ;
   nnn_21_in = 1 ;
   nnn_22_in = 1 ;
 }
 if ( CFAE::AccountFreeMargin()<10.0 )
 {
   nnn_23_bo = false ;
   Print(TradeComment + " " + nnn_1_st,": Not enough money: ",DoubleToString(MathFloor(CFAE::AccountFreeMargin()),2)); 
 }
 if ( ( UID > 9 || UID <  0 ) )
 {
   Print(TradeComment + " " + nnn_1_st,": UID value issue!"); 
   nnn_23_bo = false ;
 }
 gainkit[uuu_0_in].da_7 = CFAE::iTime(nnn_1_st,mmm_21_in,0);
 gainkit[uuu_0_in].da_8 = gainkit[uuu_0_in].da_7;
 nnn_31_da = gainkit[uuu_0_in].da_7 ;
 if ( gainkit[uuu_0_in].in_4 <  0x2 )
 {
   nnn_23_bo = false ;
 }
 if ( !(AllowOpeningNewGrid) )
 {
   nnn_23_bo = false ;
 }
 if ( !(mmm_37_bo) )
 {
   nnn_23_bo = false ;
 }
 mmm_28_in = CFAE::TimeHour(nnn_31_da) ;
 nnn_32_in = CFAE::TimeMinute(nnn_31_da) ;
 nnn_33_in = CFAE::TimeDayOfWeek(nnn_31_da) ;
 nnn_34_in = CFAE::TimeMonth(nnn_31_da) ;
 nnn_35_in = CFAE::TimeDay(nnn_31_da) ;
 nnn_36_in = CFAE::TimeDayOfWeek(nnn_31_da) ;
 nnn_37_in = CFAE::TimeYear(nnn_31_da) ;
 gainkit[uuu_0_in].bo_5 = nnn_23_bo;
 gainkit[uuu_0_in].bo_6 = nnn_23_bo;
 gainkit[uuu_0_in].bo_10 = false;
 nnn_38_in = SymbolInfoInteger(nnn_1_st,30) ;
 switch(nnn_38_in)
 {
   case 0 :
   Print(TradeComment + " " + nnn_1_st,": Trading is disabled for ",nnn_1_st); 
   gainkit[uuu_0_in].bo_5 = false;
   gainkit[uuu_0_in].bo_6 = false;
     break;
   case 3 :
   gainkit[uuu_0_in].bo_5 = true;
   gainkit[uuu_0_in].bo_6 = false;
     break;
   case 4 :
   gainkit[uuu_0_in].bo_5 = false;
   gainkit[uuu_0_in].bo_6 = true;
     break;
   case 1 :
   gainkit[uuu_0_in].bo_5 = false;
   gainkit[uuu_0_in].bo_6 = false;
 }
 if ( AllowToBuySell == 1 )
 {
   gainkit[uuu_0_in].bo_5 = true;
   gainkit[uuu_0_in].bo_6 = false;
 }
 if ( AllowToBuySell == 2 )
 {
   gainkit[uuu_0_in].bo_5 = false;
   gainkit[uuu_0_in].bo_6 = true;
 }
 gainkit[uuu_0_in].do_9 = CFAE::iClose(nnn_1_st,mmm_21_in,1);
 gainkit[uuu_0_in].bo_5 &=AllowOpeningNewGrid;
 gainkit[uuu_0_in].bo_6 &=AllowOpeningNewGrid;
 nnn_39_bo = true ;
 nnn_40_in = 0 ;
 nnn_41_in = 0 ;
 nnn_42_in = 0 ;
 nnn_43_in = 0 ;
 nnn_44_in = 59 ;
 nnn_40_in=nnn_32_in + mmm_28_in * 100;
 nnn_41_in=HourToStartTrading * 100;
 nnn_42_in=HourToStopTrading * 100 + 59;
 if ( nnn_42_in >= nnn_41_in )
 {
   nnn_39_bo &= nnn_40_in>=nnn_41_in && nnn_40_in<=nnn_42_in;
 }
 if ( nnn_42_in <  nnn_41_in )
 {
   nnn_39_bo &= nnn_40_in>=nnn_41_in && nnn_40_in<=nnn_42_in;
 }
 nnn_45_in = 5 ;
 if ( AllowTradingOnHolidays )
 {
   nnn_45_in = 0 ;
 }
 if ( nnn_45_in >  0 && ( nnn_34_in == 1 || nnn_34_in == 12 ) && nnn_45_in <  31 )
 {
   if ( nnn_34_in == 12 && nnn_35_in >  31 - nnn_45_in )
   {
     nnn_39_bo = false ;
   }
   if ( nnn_34_in == 1 && nnn_35_in <= nnn_45_in )
   {
     nnn_39_bo = false ;
   }
 }
 nnn_39_bo &=nnn_32_in==0 || nnn_32_in==15 || nnn_32_in==30 || nnn_32_in==45;
 gainkit[uuu_0_in].bo_5 &=nnn_39_bo;
 gainkit[uuu_0_in].bo_6 &=nnn_39_bo;
 CFAE::HideTestIndicators(true); 
 nnn_46_do = (CFAE::iStdDev(nnn_1_st,lizong_10(mmm_21_in),BollingerBandsPeriod + 1,0,0,0,1)) * 2.0 + CFAE::iMA(nnn_1_st,lizong_10(mmm_21_in),BollingerBandsPeriod + 1,0,0,0,1) ;
 nnn_47_do = CFAE::iMA(nnn_1_st,lizong_10(mmm_21_in),BollingerBandsPeriod + 1,0,0,0,1) - ((CFAE::iStdDev(nnn_1_st,lizong_10(mmm_21_in),BollingerBandsPeriod + 1,0,0,0,1)) * 2.0) ;
 CFAE::HideTestIndicators(false); 
 nnn_46_do = NormalizeDouble(nnn_46_do,CFAE::MarketInfo(nnn_1_st,12)) ;
 nnn_47_do = NormalizeDouble(nnn_47_do,CFAE::MarketInfo(nnn_1_st,12)) ;
 nnn_48_do = CFAE::iHigh(nnn_1_st,lizong_10(mmm_21_in),CFAE::iHighest(nnn_1_st,lizong_10(mmm_21_in),2,BollingerBandsPeriod + 1,2)) ;
 nnn_49_do = CFAE::iLow(nnn_1_st,lizong_10(mmm_21_in),CFAE::iLowest(nnn_1_st,lizong_10(mmm_21_in),1,BollingerBandsPeriod + 1,2)) ;
 nnn_48_do = NormalizeDouble(nnn_48_do,CFAE::MarketInfo(nnn_1_st,12)) ;
 nnn_49_do = NormalizeDouble(nnn_49_do,CFAE::MarketInfo(nnn_1_st,12)) ;
 gainkit[uuu_0_in].do_13 = nnn_46_do - nnn_47_do;
 if ( RSI_Period != 0 && RSI_Value >  0 )
 {
   nnn_50_do = CFAE::iRSI(nnn_1_st,lizong_10(mmm_21_in),RSI_Period,0,1) ;
   nnn_50_do = NormalizeDouble(nnn_50_do,CFAE::MarketInfo(nnn_1_st,12)) ;
   gainkit[uuu_0_in].bo_5 &=nnn_50_do<50 - RSI_Value;
   gainkit[uuu_0_in].bo_6 &=nnn_50_do>RSI_Value + 50;
 }
 gainkit[uuu_0_in].bo_5 &=gainkit[uuu_0_in].do_9<nnn_49_do;
 gainkit[uuu_0_in].bo_5 &=nnn_49_do>0.0;
 gainkit[uuu_0_in].bo_6 &=gainkit[uuu_0_in].do_9>nnn_48_do;
 gainkit[uuu_0_in].bo_6 &=nnn_48_do>0.0;
 ppp_in_10 = 0;
 for (ppp_in_11 = 0 ; ppp_in_11 < ArraySize(gainkit) ; ppp_in_11=ppp_in_11 + 1)
 {
   if ( lizong_21(gainkit[ppp_in_11].st_1,0,0) )
   {
     ppp_in_10=ppp_in_10 + 1;
   }
 }
 if ( ppp_in_10 >= MaximumSymbols )
 {
   gainkit[uuu_0_in].bo_5 = false;
   gainkit[uuu_0_in].bo_6 = false;
 }
 if ( SmartDistance )
 {
   nnn_51_do = CFAE::iATR(nnn_1_st,mmm_21_in,96,1) ;
   nnn_52_do = CFAE::iATR(nnn_1_st,mmm_21_in,672,1) ;
   if ( nnn_52_do>mmm_25_do )
   {
     gainkit[uuu_0_in].do_12 = nnn_51_do / nnn_52_do;
   }
   if ( gainkit[uuu_0_in].do_12<1.0 )
   {
     gainkit[uuu_0_in].do_12 = 1.0;
   }
   if ( gainkit[uuu_0_in].do_12>1.5 )
   {
     gainkit[uuu_0_in].do_12 = 1.5;
   }
 }
 if ( nnn_36_in != gainkit[uuu_0_in].in_21 && gainkit[uuu_0_in].in_21 != 0x0 )
 {
   gainkit[uuu_0_in].bo_19 = gainkit[uuu_0_in].bo_20;
   gainkit[uuu_0_in].bo_20 = true;
 }
 gainkit[uuu_0_in].in_21 = nnn_36_in;
 gainkit[uuu_0_in].bo_5 &=gainkit[uuu_0_in].bo_19;
 gainkit[uuu_0_in].bo_6 &=gainkit[uuu_0_in].bo_19;
 if ( mmm_11_bo && nnn_37_in * 10000 + nnn_34_in * 100 + nnn_35_in <  20211020 )
 {
   lizong_28(uuu_0_in); 
 }
 mmm_5_in ++;
 mmm_5_in ++;
 lizong_29(); 
 if ( MinimumFreeMargin>mmm_25_do && AccountInfoDouble(ACCOUNT_MARGIN_LEVEL)<MinimumFreeMargin && AccountInfoDouble(ACCOUNT_MARGIN_LEVEL)>mmm_25_do )
 {
   for (ppp_in_12 = 0 ; ppp_in_12 < ArraySize(gainkit) ; ppp_in_12=ppp_in_12 + 1)
   {
     gainkit[ppp_in_12].bo_5 = false;
     gainkit[ppp_in_12].bo_6 = false;
   }
   if ( TimeCurrent() - mmm_34_lo >  1800 )
   {
     Print(TradeComment + " " + "->",": Too low account margin level: ",DoubleToString(AccountInfoDouble(ACCOUNT_MARGIN_LEVEL),2),". Trading is not allowed!"); 
     mmm_34_lo = TimeCurrent() ;
   }
 }
 if ( mmm_32_in != mmm_28_in )
 {
   mmm_30_in --;
 }
 if ( mmm_30_in <  0 )
 {
   mmm_30_in = 0 ;
 }
 if ( mmm_29_bo )
 {
   nnn_53_do = 0.0 ;
   for (nnn_54_in = 0 ; nnn_54_in < ArraySize(gainkit) ; nnn_54_in ++)
   {
     nnn_53_do = nnn_53_do + lizong_24(gainkit[nnn_54_in].st_1,-1,0,false) ;
   }
   if ( nnn_53_do<mmm_25_do )
   {
     mmm_29_bo = false ;
   }
 }
 if ( mmm_29_bo )
 {
   gainkit[uuu_0_in].bo_5 = false;
   gainkit[uuu_0_in].bo_6 = false;
   if ( TimeCurrent() - mmm_33_lo >  3600 )
   {
     Print(TradeComment + " " + gainkit[uuu_0_in].st_1,": Trading not allowed: got a signal to close all trades!"); 
     mmm_33_lo = TimeCurrent() ;
   }
 }
 if ( mmm_31_bo )
 {
   gainkit[uuu_0_in].bo_5 = false;
   gainkit[uuu_0_in].bo_6 = false;
   if ( TimeCurrent() - mmm_33_lo >  3600 )
   {
     Print(TradeComment + " " + gainkit[uuu_0_in].st_1,": Max DD reached: trading not allowed until restart!"); 
     mmm_33_lo = TimeCurrent() ;
   }
 }
 if ( mmm_30_in >  0 )
 {
   gainkit[uuu_0_in].bo_5 = false;
   gainkit[uuu_0_in].bo_6 = false;
   if ( TimeCurrent() - mmm_33_lo >  3600 )
   {
     Print(TradeComment + " " + gainkit[uuu_0_in].st_1,": Max DD reached: trading is not allowed for ",IntegerToString(mmm_30_in,0,32)," hour(s)!"); 
     mmm_33_lo = TimeCurrent() ;
   }
 }
 mmm_32_in = mmm_28_in ;
 lizong_33(uuu_0_in,false); 
 }
//lizong_32 <<==--------   --------
 void lizong_33( int uuu_0_in,bool uuu_1_bo)
 {
  string    nnn_1_st;
  double    nnn_2_do;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  bool      nnn_6_bo;
  double    nnn_7_do;
  double    nnn_8_do;
  double    nnn_9_do;
  double    nnn_10_do;
  int       nnn_11_in;
  double    nnn_12_do;
  int       nnn_13_in;
  double    nnn_14_do;
  long      nnn_16_lo;
  double    nnn_17_do;
  int       nnn_18_in;
  int       nnn_19_in;
  bool      nnn_20_bo;
  double    nnn_21_do;
  double    nnn_22_do;
  double    nnn_23_do;
  double    nnn_24_do;
  int       nnn_25_in;
  double    nnn_26_do;
  int       nnn_27_in;
  double    nnn_28_do;
  long      nnn_30_lo;
  int       nnn_31_in;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;
 int        ppp_in_3;
 bool       ppp_bo_4;
 int        ppp_in_5;
 int        ppp_in_6;
 double     ppp_do_7;
 double     ppp_do_8;
 double     ppp_do_9;
 double     ppp_do_10;
 int        ppp_in_11;
 double     ppp_do_12;
 int        ppp_in_13;
 int        ppp_in_14;
 string     ppp_st_15;
 string     ppp_st_16;
 double     ppp_do_17;
 double     ppp_do_18;
 int        ppp_in_19;
 int        ppp_in_20;
 long       ppp_lo_21;
 int        ppp_in_22;
 int        ppp_in_23;
 bool       ppp_bo_24;
 int        ppp_in_25;
 int        ppp_in_26;
 double     ppp_do_27;
 double     ppp_do_28;
 double     ppp_do_29;
 double     ppp_do_30;
 int        ppp_in_31;
 double     ppp_do_32;
 int        ppp_in_33;
 int        ppp_in_34;
 string     ppp_st_35;
 string     ppp_st_36;
 double     ppp_do_37;
 double     ppp_do_38;
 int        ppp_in_39;
 int        ppp_in_40;
 long       ppp_lo_41;

 nnn_1_st = gainkit[uuu_0_in].st_1 ;
 ppp_in_1 = TerminalInfoInteger(8);
 if ( ppp_in_1 != 0 )
 {
   ppp_in_1 = AccountInfoInteger(ACCOUNT_TRADE_EXPERT);
 }
 if ( ppp_in_1 != 0 )
 {
   ppp_in_1 = MQLInfoInteger(MQL_TRADE_ALLOWED);
 }
 if ( ppp_in_1 == 0 && !(CFAE::IsTesting()) && CFAE::IsOptimization() )
 {
   if ( ( gainkit[uuu_0_in].bo_5 != 0x0 || gainkit[uuu_0_in].bo_6 != 0x0 ) )
   {
     Print(TradeComment + " " + nnn_1_st,": Trading is not allowed!"); 
   }
   return;
 }
 if ( gainkit[uuu_0_in].bo_5 != 0x0 )
 {
   CFAE::RefreshRates(); 
   nnn_2_do = CFAE::MarketInfo(nnn_1_st,13) ;
   if ( ( ( !(lizong_21(nnn_1_st,-1,1)) && AllowHedging ) || (!(lizong_21(nnn_1_st,-1,0)) && !(AllowHedging)) ) )
   {
     ppp_in_2 = 0;
     for (ppp_in_3 = 0 ; ppp_in_3 < ArraySize(gainkit) ; ppp_in_3=ppp_in_3 + 1)
     {
       if ( lizong_21(gainkit[ppp_in_3].st_1,0,0) )
       {
         ppp_in_2=ppp_in_2 + 1;
       }
     }
     if ( ppp_in_2 <  MaximumSymbols )
     {
       nnn_3_in = 0 ;
       nnn_4_in = 10 ;
       nnn_5_in = 0 ;
       nnn_6_bo = false ;
         if(!(IsStopped())){
       do
       {
         CFAE::RefreshRates(); 
         nnn_7_do = CFAE::MarketInfo(nnn_1_st,10) ;
         nnn_8_do = lizong_34(nnn_1_st,true) ;
         if ( nnn_8_do<mmm_25_do )
         {
           Print(TradeComment + " " + nnn_1_st,": Sending stopped because los size is too small: ",DoubleToString(nnn_8_do,8)); 
           return;
         }
         if ( CFAE::IsTesting() )
         {
           ppp_bo_4 = true;
         }
         else
         {
           if ( TerminalInfoInteger(6) == 0 )
           {
             gainkit[uuu_0_in].bo_5 = false;
             gainkit[uuu_0_in].bo_6 = false;
             Print(TradeComment + " " + gainkit[uuu_0_in].st_1,": Signal rejected due to absence of network connection!"); 
             ppp_bo_4 = false;
           }
           else
           {
             ppp_bo_4 = true;
           }
         }
         if ( !(ppp_bo_4) && !(CFAE::IsTesting()) )
         {
           Print(TradeComment + " " + nnn_1_st,": No connection to trading server!"); 
           return;
         }
         nnn_9_do = CFAE::AccountFreeMarginCheck(nnn_1_st,0,nnn_8_do) ;
         if ( nnn_9_do<=0.0 )
         {
           Print(TradeComment + " " + nnn_1_st,": Not enough money to send a new initial buy order: ",DoubleToString(nnn_9_do,2)); 
           gainkit[uuu_0_in].bo_5 = false;
           nnn_6_bo = true ;
         }
         else
         {
           Print(TradeComment + " " + nnn_1_st,": Sending a new initial buy order, attempt N",IntegerToString(nnn_3_in + 1,0,32)); 
           ppp_in_5 = 10;
           ppp_in_6 = CFAE::MarketInfo(nnn_1_st,12);
           if ( ppp_in_6 == 5 )
           {
             ppp_in_5 = 10;
           }
           if ( ppp_in_6 == 4 )
           {
             ppp_in_5 = 1;
           }
           if ( ppp_in_6 == 0x3 )
           {
             ppp_in_5 = 10;
           }
           if ( ( ppp_in_6 == 2 || ppp_in_6 == 1 || ppp_in_6 == 0 ) )
           {
             ppp_in_5 = 1;
           }
           if ( ( nnn_2_do<MaximumSpread * ppp_in_5 || MaximumSpread<mmm_25_do ) )
           {
             ppp_do_7 = SymbolInfoDouble(nnn_1_st,35);
             ppp_do_8 = SymbolInfoDouble(nnn_1_st,36);
             if ( ppp_do_7>SymbolInfoDouble(nnn_1_st,55) && SymbolInfoDouble(nnn_1_st,55)>mmm_25_do )
             {
               ppp_do_7 = SymbolInfoDouble(nnn_1_st,55);
             }
             if ( ppp_do_7>MaximumLot )
             {
               ppp_do_7 = MaximumLot;
             }
             if ( ppp_do_8<0.001001 && ppp_do_8>0.000999 )
             {
               ppp_do_7 = NormalizeDouble(ppp_do_7,3);
             }
             if ( ppp_do_8<0.010001 && ppp_do_8>0.009999 )
             {
               ppp_do_7 = NormalizeDouble(ppp_do_7,2);
             }
             if ( ppp_do_8<0.100001 && ppp_do_8>0.099999 )
             {
               ppp_do_7 = NormalizeDouble(ppp_do_7,1);
             }
             if ( ppp_do_8<1.000001 && ppp_do_8>0.999999 )
             {
               ppp_do_7 = NormalizeDouble(ppp_do_7,0);
             }
             nnn_10_do = ppp_do_7 ;
             nnn_11_in = 1 ;
             if ( nnn_8_do>nnn_10_do && AutoSplit )
             {
               nnn_11_in = MathCeil(nnn_8_do / nnn_10_do) ;
             }
             nnn_12_do = nnn_8_do ;
             for (nnn_13_in = 0 ; nnn_13_in < nnn_11_in ; nnn_13_in ++)
             {
               nnn_14_do = MathMin(nnn_10_do,nnn_12_do) ;
               ppp_do_9 = nnn_14_do;
               ppp_do_10 = SymbolInfoDouble(nnn_1_st,36);
               if ( ppp_do_10<0.001001 && ppp_do_10>0.000999 )
               {
                 ppp_do_9 = NormalizeDouble(ppp_do_9,3);
               }
               if ( ppp_do_10<0.010001 && ppp_do_10>0.009999 )
               {
                 ppp_do_9 = NormalizeDouble(ppp_do_9,2);
               }
               if ( ppp_do_10<0.100001 && ppp_do_10>0.099999 )
               {
                 ppp_do_9 = NormalizeDouble(ppp_do_9,1);
               }
               if ( ppp_do_10<1.000001 && ppp_do_10>0.999999 )
               {
                 ppp_do_9 = NormalizeDouble(ppp_do_9,0);
               }
               nnn_14_do = ppp_do_9 ;
               ppp_in_11 = -1;
               ppp_do_12 = 0.0;
               ppp_in_13 = int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32))  + 2)) + (mmm_24_in + UID) * 100;
               ppp_in_14 = 0;
               ppp_st_15 = TradeComment;
               if ( uuu_1_bo )
               {
                 ppp_st_15 = TradeComment + " M";
               }
               if ( ppp_in_14 >  0 )
               {
                 ppp_st_15 = ppp_st_15 + " #" + string(ppp_in_14);
               }
               ppp_st_16 = ppp_st_15;
               ppp_do_17 = 0.0;
               ppp_do_18 = 0.0;
               ppp_in_19 = 10;
               ppp_in_20 = CFAE::MarketInfo(nnn_1_st,12);
               if ( ppp_in_20 == 5 )
               {
                 ppp_in_19 = 10;
               }
               if ( ppp_in_20 == 4 )
               {
                 ppp_in_19 = 1;
               }
               if ( ppp_in_20 == 0x3 )
               {
                 ppp_in_19 = 10;
               }
               if ( ( ppp_in_20 == 2 || ppp_in_20 == 1 || ppp_in_20 == 0 ) )
               {
                 ppp_in_19 = 1;
               }
               nnn_16_lo = CFAE::OrderSend(nnn_1_st,0,nnn_14_do,nnn_7_do,int(MaximumSlippage * ppp_in_19),ppp_do_18,ppp_do_17,ppp_st_16,ppp_in_13,ppp_do_12,ppp_in_11) ;
               if ( nnn_16_lo <  0 )
               {
                 nnn_5_in = CFAE::GetLastError() ;
                 Print(TradeComment + " " + nnn_1_st,": Failed to send a new initial buy order. Error:",lizong_11(nnn_5_in)); 
                 if ( nnn_5_in == 4110 && CFAE::IsTesting() )
                 {
                   nnn_6_bo = true ;
                 }
                 if ( nnn_5_in == 149 )
                 {
                   nnn_6_bo = true ;
                   gainkit[uuu_0_in].bo_5 = false;
                 }
                 if ( ( nnn_5_in == 148 || nnn_5_in == 139 || nnn_5_in == 134 || nnn_5_in == 133 || nnn_5_in == 128 || nnn_5_in == 64 || nnn_5_in == 6 || nnn_5_in == 4 || nnn_5_in == 3 || nnn_5_in == 2 || nnn_5_in == 1 ) )
                 {
                   nnn_6_bo = true ;
                   gainkit[uuu_0_in].bo_5 = false;
                   Print(TradeComment + " " + nnn_1_st,": Stopped trying to send a new initial buy order due to fatal error!"); 
                 }
                 Sleep(5000); 
               }
               else
               {
                 Print(TradeComment + " " + nnn_1_st,": Initial buy trade is opened id: ",IntegerToString(nnn_16_lo,0,32)); 
                 nnn_6_bo = true ;
                 gainkit[uuu_0_in].bo_5 = false;
                 gainkit[uuu_0_in].bo_10 = true;
                 gainkit[uuu_0_in].bo_11 = true;
                 gainkit[uuu_0_in].da_27 = TimeCurrent();
               }
               nnn_12_do = nnn_12_do - nnn_14_do ;
               Sleep(500); 
             }
           }
           else
           {
             Print(TradeComment + " " + nnn_1_st,": Cannot open a new initial buy trade due to high spread: ",DoubleToString(nnn_2_do,2)); 
             Sleep(5000); 
           }
         }
         if ( !(CFAE::IsTesting()) && !(CFAE::IsOptimization()) )
         {
           ppp_lo_21 = TerminalInfoInteger(8);
           if ( ppp_lo_21 != 0 )
           {
             ppp_lo_21 = AccountInfoInteger(ACCOUNT_TRADE_EXPERT);
           }
           if ( ppp_lo_21 != 0 )
           {
             ppp_lo_21 = MQLInfoInteger(MQL_TRADE_ALLOWED);
           }
           if ( ppp_lo_21 == 0 )
           {
             nnn_6_bo = true ;
           }
         }
         if ( nnn_3_in >= nnn_4_in )
         {
           nnn_6_bo = true ;
         }
         nnn_3_in ++;
         if ( IsStopped() )   break;
         
       }
       while(!(nnn_6_bo));
       }
     }
   }
 }
 if ( gainkit[uuu_0_in].bo_6 != 0x0 )
 {
   CFAE::RefreshRates(); 
   nnn_17_do = CFAE::MarketInfo(nnn_1_st,13) ;
   if ( ( ( !(lizong_21(nnn_1_st,-1,-1)) && AllowHedging ) || (!(lizong_21(nnn_1_st,-1,0)) && !(AllowHedging)) ) )
   {
     ppp_in_22 = 0;
     for (ppp_in_23 = 0 ; ppp_in_23 < ArraySize(gainkit) ; ppp_in_23=ppp_in_23 + 1)
     {
       if ( lizong_21(gainkit[ppp_in_23].st_1,0,0) )
       {
         ppp_in_22=ppp_in_22 + 1;
       }
     }
     if ( ppp_in_22 <  MaximumSymbols )
     {
       nnn_18_in = 0 ;
       nnn_19_in = 10 ;
       nnn_20_bo = false ;
         if(!(IsStopped())){
       do
       {
         CFAE::RefreshRates(); 
         nnn_21_do = CFAE::MarketInfo(nnn_1_st,9) ;
         nnn_22_do = lizong_34(nnn_1_st,true) ;
         if ( nnn_22_do<mmm_25_do )
         {
           Print(TradeComment + " " + nnn_1_st,": Sending stopped because lot size is too small: ",DoubleToString(nnn_22_do,8)); 
           return;
         }
         if ( CFAE::IsTesting() )
         {
           ppp_bo_24 = true;
         }
         else
         {
           if ( TerminalInfoInteger(6) == 0 )
           {
             gainkit[uuu_0_in].bo_5 = false;
             gainkit[uuu_0_in].bo_6 = false;
             Print(TradeComment + " " + gainkit[uuu_0_in].st_1,": Signal rejected due to absence of network connection!"); 
             ppp_bo_24 = false;
           }
           else
           {
             ppp_bo_24 = true;
           }
         }
         if ( !(ppp_bo_24) && !(CFAE::IsTesting()) )
         {
           Print(TradeComment + " " + nnn_1_st,": No connection to trading server!"); 
           return;
         }
         nnn_23_do = CFAE::AccountFreeMarginCheck(nnn_1_st,1,nnn_22_do) ;
         if ( nnn_23_do<=0.0 )
         {
           Print(TradeComment + " " + nnn_1_st,": Not enough money to send a new initial sell order: ",DoubleToString(nnn_23_do,2)); 
           gainkit[uuu_0_in].bo_6 = false;
           nnn_20_bo = true ;
         }
         else
         {
           Print(TradeComment + " " + nnn_1_st,": Sending a new initial sell order, attempt N",IntegerToString(nnn_18_in + 1,0,32)); 
           ppp_in_25 = 10;
           ppp_in_26 = CFAE::MarketInfo(nnn_1_st,12);
           if ( ppp_in_26 == 5 )
           {
             ppp_in_25 = 10;
           }
           if ( ppp_in_26 == 4 )
           {
             ppp_in_25 = 1;
           }
           if ( ppp_in_26 == 0x3 )
           {
             ppp_in_25 = 10;
           }
           if ( ( ppp_in_26 == 2 || ppp_in_26 == 1 || ppp_in_26 == 0 ) )
           {
             ppp_in_25 = 1;
           }
           if ( ( nnn_17_do<MaximumSpread * ppp_in_25 || MaximumSpread<mmm_25_do ) )
           {
             ppp_do_27 = SymbolInfoDouble(nnn_1_st,35);
             ppp_do_28 = SymbolInfoDouble(nnn_1_st,36);
             if ( ppp_do_27>SymbolInfoDouble(nnn_1_st,55) && SymbolInfoDouble(nnn_1_st,55)>mmm_25_do )
             {
               ppp_do_27 = SymbolInfoDouble(nnn_1_st,55);
             }
             if ( ppp_do_27>MaximumLot )
             {
               ppp_do_27 = MaximumLot;
             }
             if ( ppp_do_28<0.001001 && ppp_do_28>0.000999 )
             {
               ppp_do_27 = NormalizeDouble(ppp_do_27,3);
             }
             if ( ppp_do_28<0.010001 && ppp_do_28>0.009999 )
             {
               ppp_do_27 = NormalizeDouble(ppp_do_27,2);
             }
             if ( ppp_do_28<0.100001 && ppp_do_28>0.099999 )
             {
               ppp_do_27 = NormalizeDouble(ppp_do_27,1);
             }
             if ( ppp_do_28<1.000001 && ppp_do_28>0.999999 )
             {
               ppp_do_27 = NormalizeDouble(ppp_do_27,0);
             }
             nnn_24_do = ppp_do_27 ;
             nnn_25_in = 1 ;
             if ( nnn_22_do>nnn_24_do && AutoSplit )
             {
               nnn_25_in = MathCeil(nnn_22_do / nnn_24_do) ;
             }
             nnn_26_do = nnn_22_do ;
             for (nnn_27_in = 0 ; nnn_27_in < nnn_25_in ; nnn_27_in ++)
             {
               nnn_28_do = MathMin(nnn_24_do,nnn_26_do) ;
               ppp_do_29 = nnn_28_do;
               ppp_do_30 = SymbolInfoDouble(nnn_1_st,36);
               if ( ppp_do_30<0.001001 && ppp_do_30>0.000999 )
               {
                 ppp_do_29 = NormalizeDouble(ppp_do_29,3);
               }
               if ( ppp_do_30<0.010001 && ppp_do_30>0.009999 )
               {
                 ppp_do_29 = NormalizeDouble(ppp_do_29,2);
               }
               if ( ppp_do_30<0.100001 && ppp_do_30>0.099999 )
               {
                 ppp_do_29 = NormalizeDouble(ppp_do_29,1);
               }
               if ( ppp_do_30<1.000001 && ppp_do_30>0.999999 )
               {
                 ppp_do_29 = NormalizeDouble(ppp_do_29,0);
               }
               nnn_28_do = ppp_do_29 ;
               ppp_in_31 = -1;
               ppp_do_32 = 0.0;
               ppp_in_33 = (int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32))  + 2))) * 2 + (mmm_24_in + UID) * 100;
               ppp_in_34 = 0;
               ppp_st_35 = TradeComment;
               if ( uuu_1_bo )
               {
                 ppp_st_35 = TradeComment + " M";
               }
               if ( ppp_in_34 >  0 )
               {
                 ppp_st_35 = ppp_st_35 + " #" + string(ppp_in_34);
               }
               ppp_st_36 = ppp_st_35;
               ppp_do_37 = 0.0;
               ppp_do_38 = 0.0;
               ppp_in_39 = 10;
               ppp_in_40 = CFAE::MarketInfo(nnn_1_st,12);
               if ( ppp_in_40 == 5 )
               {
                 ppp_in_39 = 10;
               }
               if ( ppp_in_40 == 4 )
               {
                 ppp_in_39 = 1;
               }
               if ( ppp_in_40 == 0x3 )
               {
                 ppp_in_39 = 10;
               }
               if ( ( ppp_in_40 == 2 || ppp_in_40 == 1 || ppp_in_40 == 0 ) )
               {
                 ppp_in_39 = 1;
               }
               nnn_30_lo = CFAE::OrderSend(nnn_1_st,1,nnn_28_do,nnn_21_do,int(MaximumSlippage * ppp_in_39),ppp_do_38,ppp_do_37,ppp_st_36,ppp_in_33,ppp_do_32,ppp_in_31) ;
               if ( nnn_30_lo <  0 )
               {
                 nnn_31_in = CFAE::GetLastError() ;
                 Print(TradeComment + " " + nnn_1_st,": Failed to send a new initial sell order. Error:",lizong_11(nnn_31_in)); 
                 if ( nnn_31_in == 0x100F && CFAE::IsTesting() )
                 {
                   nnn_20_bo = true ;
                 }
                 if ( nnn_31_in == 149 )
                 {
                   nnn_20_bo = true ;
                   gainkit[uuu_0_in].bo_6 = false;
                 }
                 if ( ( nnn_31_in == 148 || nnn_31_in == 0x8B || nnn_31_in == 134 || nnn_31_in == 133 || nnn_31_in == 128 || nnn_31_in == 64 || nnn_31_in == 6 || nnn_31_in == 4 || nnn_31_in == 0x3 || nnn_31_in == 2 || nnn_31_in == 1 ) )
                 {
                   nnn_20_bo = true ;
                   gainkit[uuu_0_in].bo_6 = false;
                   Print(TradeComment + " " + nnn_1_st,": Stopped trying to send a new initial sell order due to fatal error!"); 
                 }
                 Sleep(5000); 
               }
               else
               {
                 Print(TradeComment + " " + nnn_1_st,": Initial sell trade is opened, id: ",IntegerToString(nnn_30_lo,0,32)); 
                 nnn_20_bo = true ;
                 gainkit[uuu_0_in].bo_6 = false;
                 gainkit[uuu_0_in].bo_10 = true;
                 gainkit[uuu_0_in].bo_11 = true;
                 gainkit[uuu_0_in].da_28 = TimeCurrent();
               }
               nnn_26_do = nnn_26_do - nnn_28_do ;
               Sleep(500); 
             }
           }
           else
           {
             Print(TradeComment + " " + nnn_1_st,": Cannot open a new initial sell trade due to high spread: ",DoubleToString(nnn_17_do,2)); 
             Sleep(5000); 
           }
         }
         if ( !(CFAE::IsTesting()) && !(CFAE::IsOptimization()) )
         {
           ppp_lo_41 = TerminalInfoInteger(8);
           if ( ppp_lo_41 != 0 )
           {
             ppp_lo_41 = AccountInfoInteger(ACCOUNT_TRADE_EXPERT);
           }
           if ( ppp_lo_41 != 0 )
           {
             ppp_lo_41 = MQLInfoInteger(MQL_TRADE_ALLOWED);
           }
           if ( ppp_lo_41 == 0 )
           {
             nnn_20_bo = true ;
           }
         }
         if ( nnn_18_in >= nnn_19_in )
         {
           nnn_20_bo = true ;
         }
         nnn_18_in ++;
         if ( IsStopped() )   break;
         
       }
       while(!(nnn_20_bo));
       }
     }
   }
 }
 }
//lizong_33 <<==--------   --------
 double lizong_34( string uuu_0_st,bool uuu_1_bo)
 {
  double    nnn_1_do;
  double    nnn_2_do;
  double    nnn_3_do;
  double    nnn_4_do;
  double    nnn_5_do;
  double    nnn_6_do;
  double    nnn_7_do;
  double    nnn_8_do;
  double    nnn_9_do;
  double    nnn_10_do;
  double    nnn_11_do;
  double    nnn_12_do;
  double    nnn_13_do;
  double    nnn_14_do;
  int       nnn_15_in;
  int       nnn_16_in;
  int       nnn_17_in;
  int       nnn_18_in;
  int       nnn_19_in;
  int       nnn_20_in;
  int       nnn_21_in;
  int       nnn_22_in;
  double    nnn_23_do;
  int       nnn_24_in;
  int       nnn_25_in;
  double    nnn_26_do;
//----- -----

 nnn_2_do = SymbolInfoDouble(uuu_0_st,36) ;
 nnn_3_do = SymbolInfoDouble(uuu_0_st,34) ;
 nnn_4_do = SymbolInfoDouble(uuu_0_st,35) ;
 nnn_5_do = (CFAE::MarketInfo(uuu_0_st,11)>mmm_25_do) ?CFAE::MarketInfo(uuu_0_st,11):0.00001  ;
 if ( nnn_2_do<0.0001 )
 {
   nnn_2_do = 0.001 ;
 }
 nnn_6_do = CFAE::AccountFreeMargin() ;
 nnn_7_do = AccountInfoDouble(ACCOUNT_BALANCE) ;
 nnn_8_do = AccountInfoDouble(ACCOUNT_EQUITY) ;
 if ( FixedInitialDeposit && CFAE::IsTesting() && mmm_38_do>mmm_25_do )
 {
   nnn_6_do = mmm_38_do ;
   nnn_7_do = mmm_38_do ;
   nnn_8_do = mmm_38_do ;
 }
 nnn_9_do = CFAE::MarketInfo(uuu_0_st,32) ;
 nnn_10_do = AccountInfoInteger(ACCOUNT_LEVERAGE) ;
 if ( nnn_9_do<mmm_25_do && uuu_0_st != "??????" )
 {
   Sleep(100); 
   nnn_9_do = CFAE::MarketInfo(uuu_0_st,32) ;
   if ( nnn_9_do<mmm_25_do )
   {
     Print(TradeComment + " " + uuu_0_st,": Failed to get MODE_MARGINREQUIRED. Trying to get it again #2"); 
     Sleep(1000); 
     nnn_9_do = CFAE::MarketInfo(uuu_0_st,32) ;
   }
   if ( nnn_9_do<mmm_25_do )
   {
     Print(TradeComment + " " + uuu_0_st,": Failed to get MODE_MARGINREQUIRED. Trying to get it again #3"); 
     Sleep(2000); 
     nnn_9_do = CFAE::MarketInfo(uuu_0_st,32) ;
   }
 }
 if ( nnn_10_do<mmm_25_do && uuu_0_st != "??????" )
 {
   Sleep(100); 
   nnn_10_do = AccountInfoInteger(ACCOUNT_LEVERAGE) ;
   if ( nnn_10_do<mmm_25_do )
   {
     Print(TradeComment + " " + uuu_0_st,": Failed to get ACCOUNT_LEVERAGE. Trying to get it again #2"); 
     Sleep(1000); 
     nnn_10_do = AccountInfoInteger(ACCOUNT_LEVERAGE) ;
   }
   if ( nnn_10_do<mmm_25_do )
   {
     Print(TradeComment + " " + uuu_0_st,": Failed to get ACCOUNT_LEVERAGE. Trying to get it again #3"); 
     Sleep(2000); 
     nnn_10_do = AccountInfoInteger(ACCOUNT_LEVERAGE) ;
   }
 }
 nnn_11_do = nnn_3_do ;
 nnn_12_do = 0.0 ;
 nnn_13_do = 0.0 ;
 nnn_14_do = 0.0 ;
 if ( AccountInfoDouble(ACCOUNT_CREDIT)>0.0 )
 {
   nnn_14_do = AccountInfoDouble(ACCOUNT_CREDIT) ;
 }
 if ( LotSizingMethod == 0 )
 {
   nnn_11_do = LotSizingValueFixed ;
   nnn_13_do = 0.0 ;
 }
 if ( LotSizingMethod == 1 )
 {
   nnn_13_do = LotSizingValueDynamic ;
 }
 if ( LotSizingMethod == 2 )
 {
   nnn_13_do = -(LotSizingValueDynamic);
 }
 if ( LotSizingMethod == 6 )
 {
   nnn_13_do = 0.0 ;
   if ( LotSizingDepositLoadPercent>mmm_25_do && nnn_9_do>mmm_25_do && nnn_10_do>mmm_25_do )
   {
     nnn_11_do = MathFloor(100.0 / nnn_10_do * nnn_6_do / nnn_9_do * LotSizingDepositLoadPercent / 100.0 / nnn_2_do) * nnn_2_do ;
   }
   else
   {
     Print(TradeComment + " " + uuu_0_st,": Can\'t calculate lot size, because no data received: ACCOUNT_LEVERAGE / MODE_MARGINREQUIRED!"); 
   }
 }
 if ( LotSizingMethod == 7 )
 {
   nnn_13_do = 0.0 ;
   nnn_16_in = 0 ;
   nnn_15_in = 1073217536 ;
   if ( nnn_9_do>mmm_25_do && nnn_10_do>mmm_25_do )
   {
     nnn_11_do = MathFloor(100.0 / nnn_10_do * nnn_6_do / nnn_9_do * 1.5 / 100.0 / nnn_2_do) * nnn_2_do ;
   }
   else
   {
     Print(TradeComment + " " + uuu_0_st,": Can\'t calculate lot size, because no data received: ACCOUNT_LEVERAGE / MODE_MARGINREQUIRED!"); 
   }
 }
 if ( LotSizingMethod == 3 )
 {
   nnn_13_do = 0.0 ;
   nnn_18_in = 0 ;
   nnn_17_in = 1072693248 ;
   if ( nnn_9_do>mmm_25_do && nnn_10_do>mmm_25_do )
   {
     nnn_11_do = MathFloor(100.0 / nnn_10_do * nnn_6_do / nnn_9_do / 100.0 / nnn_2_do) * nnn_2_do ;
   }
   else
   {
     Print(TradeComment + " " + uuu_0_st,": Can\'t calculate lot size, because no data received: ACCOUNT_LEVERAGE / MODE_MARGINREQUIRED!"); 
   }
 }
 if ( LotSizingMethod == 4 )
 {
   nnn_13_do = 0.0 ;
   nnn_20_in = 0 ;
   nnn_19_in = 1071644672 ;
   if ( nnn_9_do>mmm_25_do && nnn_10_do>mmm_25_do )
   {
     nnn_11_do = MathFloor(100.0 / nnn_10_do * nnn_6_do / nnn_9_do * 0.5 / 100.0 / nnn_2_do) * nnn_2_do ;
   }
   else
   {
     Print(TradeComment + " " + uuu_0_st,": Can\'t calculate lot size, because no data received: ACCOUNT_LEVERAGE / MODE_MARGINREQUIRED!"); 
   }
 }
 if ( LotSizingMethod == 5 )
 {
   nnn_13_do = 0.0 ;
   nnn_22_in = 0 ;
   nnn_21_in = 1070596096 ;
   if ( nnn_9_do>mmm_25_do && nnn_10_do>mmm_25_do )
   {
     nnn_11_do = MathFloor(100.0 / nnn_10_do * nnn_6_do / nnn_9_do * 0.25 / 100.0 / nnn_2_do) * nnn_2_do ;
   }
   else
   {
     Print(TradeComment + " " + uuu_0_st,": Can\'t calculate lot size, because no data received: ACCOUNT_LEVERAGE / MODE_MARGINREQUIRED!"); 
   }
 }
 if ( nnn_13_do>mmm_25_do )
 {
   nnn_12_do = nnn_7_do / nnn_13_do ;
   nnn_11_do = MathRound(nnn_12_do * 0.01 / nnn_2_do) * nnn_2_do ;
 }
 if ( nnn_13_do< -(mmm_25_do) )
 {
   nnn_12_do = nnn_8_do / ( -(nnn_13_do)) ;
   nnn_11_do = MathRound(nnn_12_do * 0.01 / nnn_2_do) * nnn_2_do ;
 }
 if ( mmm_39_bo && !(AutoSplit) )
 {
   nnn_23_do = 0.0 ;
   for (nnn_24_in = 0 ; nnn_24_in < ArraySize(gainkit) ; nnn_24_in ++)
   {
     if ( gainkit[nnn_24_in].do_22>nnn_23_do )
     {
       nnn_23_do = gainkit[nnn_24_in].do_22 ;
     }
   }
   if ( (nnn_23_do + 1.0) * nnn_11_do>nnn_4_do * 2.0 && nnn_23_do + 1.0>1.0 )
   {
     nnn_11_do = nnn_4_do * 2.0 / (nnn_23_do + 1.0) ;
   }
 }
 if ( GridLevelToStart >  1 && uuu_1_bo )
 {
   nnn_11_do = nnn_3_do ;
 }
 nnn_25_in = nnn_11_do / nnn_2_do ;
 nnn_11_do = nnn_25_in * nnn_2_do ;
 if ( nnn_11_do<nnn_3_do )
 {
   nnn_11_do = nnn_3_do ;
 }
 if ( nnn_11_do>MaximumLot )
 {
   nnn_11_do = MaximumLot ;
 }
 nnn_26_do = SymbolInfoDouble(uuu_0_st,55) ;
 if ( nnn_11_do>nnn_26_do && nnn_26_do>mmm_25_do )
 {
   nnn_11_do = nnn_26_do ;
 }
 if ( nnn_11_do>nnn_4_do && !(AutoSplit) )
 {
   nnn_11_do = nnn_4_do ;
 }
 if ( nnn_2_do<0.001001 && nnn_2_do>0.000999 )
 {
   nnn_11_do = NormalizeDouble(nnn_11_do,3) ;
 }
 if ( nnn_2_do<0.010001 && nnn_2_do>0.009999 )
 {
   nnn_11_do = NormalizeDouble(nnn_11_do,2) ;
 }
 if ( nnn_2_do<0.100001 && nnn_2_do>0.099999 )
 {
   nnn_11_do = NormalizeDouble(nnn_11_do,1) ;
 }
 if ( nnn_2_do<1.000001 && nnn_2_do>0.999999 )
 {
   nnn_11_do = NormalizeDouble(nnn_11_do,0) ;
 }
 return(nnn_11_do); 
 }
//lizong_34 <<==--------   --------
 void lizong_35()
 {
  int       nnn_1_in;
  int       nnn_2_in;
  int       nnn_3_in;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;
 int        ppp_in_3;
 int        ppp_in_4;

 nnn_1_in=CFAE::Minute() + CFAE::Hour() * 100;
 if ( !(CFAE::IsTesting()) )
 {
   for (ppp_in_1 = 0 ; ppp_in_1 < ArraySize(gainkit) ; ppp_in_1=ppp_in_1 + 1)
   {
     CFAE::iTime(gainkit[ppp_in_1].st_1,mmm_21_in,0); 
     CFAE::iTime(gainkit[ppp_in_1].st_1,OPO_TimeFrame,0); 
   }
 }
 if ( ( ( HideTP && !(SmartTP) ) || HideSL || ( MaximumDrawdown>mmm_25_do && MaximumDrawdown<99.99 ) || MaximumDrawdownMoney>mmm_25_do ) )
 {
   for (nnn_2_in = 0 ; nnn_2_in < ArraySize(gainkit) ; nnn_2_in ++)
   {
     lizong_26(nnn_2_in); 
   }
 }
 if ( mmm_26_in != nnn_1_in )
 {
   if ( TimeCurrent() >  mmm_27_lo + 60 && !(CFAE::IsTesting()) && !(CFAE::IsTesting()) && !(CFAE::IsOptimization()) )
   {
     mmm_27_lo = TimeCurrent() ;
     for (ppp_in_2 = 0 ; ppp_in_2 < ArraySize(gainkit) ; ppp_in_2=ppp_in_2 + 1)
     {
       CFAE::iTime(gainkit[ppp_in_2].st_1,mmm_21_in,0); 
       CFAE::iTime(gainkit[ppp_in_2].st_1,OPO_TimeFrame,0); 
     }
     if ( ShowPanel )
     {
       lizong_49(false); 
     }
   }
   lizong_29(); 
   ppp_in_3 = TerminalInfoInteger(8);
   if ( ppp_in_3 != 0 )
   {
     ppp_in_3 = AccountInfoInteger(ACCOUNT_TRADE_EXPERT);
   }
   if ( ppp_in_3 != 0 )
   {
     ppp_in_3 = MQLInfoInteger(MQL_TRADE_ALLOWED);
   }
   if ( ( ppp_in_3 != 0 || CFAE::IsTesting() || CFAE::IsOptimization() ) )
   {
     for (nnn_3_in = 0 ; nnn_3_in < ArraySize(gainkit) ; nnn_3_in ++)
     {
       ppp_in_3 = nnn_3_in;
       if ( !(CFAE::IsTradeAllowed()) )   continue;
       ppp_in_4 = TerminalInfoInteger(8);
       if ( ppp_in_4 != 0 )
       {
         ppp_in_4 = AccountInfoInteger(ACCOUNT_TRADE_EXPERT);
       }
       if ( ppp_in_4 != 0 )
       {
         ppp_in_4 = MQLInfoInteger(MQL_TRADE_ALLOWED);
       }
       if ( ( ppp_in_4 == 0 && !(CFAE::IsTesting()) && !(CFAE::IsOptimization()) ) )   continue;
       lizong_37(ppp_in_3); 
       lizong_25(ppp_in_3); 
       lizong_26(ppp_in_3); 
       
     }
   }
 }
 if ( CFAE::IsVisualMode() )
 {
   if ( CFAE::ObjectFind(0,"but_Buy") != -1 && CFAE::ObjectGetInteger(0,"but_Buy",OBJPROP_STATE,0) != 0 )
   {
     lizong_48("but_Buy"); 
   }
   if ( CFAE::ObjectFind(0,"but_Sell") != -1 && CFAE::ObjectGetInteger(0,"but_Sell",OBJPROP_STATE,0) != 0 )
   {
     lizong_48("but_Sell"); 
   }
   if ( CFAE::ObjectFind(0,"but_Pair") != -1 && CFAE::ObjectGetInteger(0,"but_Pair",OBJPROP_STATE,0) != 0 )
   {
     lizong_48("but_Pair"); 
   }
   if ( CFAE::ObjectFind(0,"but_Suspend") != -1 )
   {
     mmm_37_bo=!(CFAE::ObjectGetInteger(0,"but_Suspend",OBJPROP_STATE,0));
     if ( CFAE::ObjectGetInteger(0,"but_Suspend",OBJPROP_STATE,0) == 0 )
     {
       CFAE::ObjectSetInteger(0,"but_Suspend",OBJPROP_BGCOLOR,32768); 
       CFAE::ObjectSetString(0,"but_Suspend",OBJPROP_TEXT,"New grids allowed"); 
     }
     if ( !(mmm_37_bo) )
     {
       CFAE::ObjectSetInteger(0,"but_Suspend",OBJPROP_BGCOLOR,255); 
       CFAE::ObjectSetString(0,"but_Suspend",OBJPROP_TEXT,"New grids NOT allowed!"); 
       ppp_in_4 = 0;
         if(ArraySize(gainkit) >  0){
       do
       {
         gainkit[ppp_in_4].bo_5 = false;
         gainkit[ppp_in_4].bo_6 = false;
       }
       while(ppp_in_4 + 1 < ArraySize(gainkit));
       }
     }
     ChartRedraw(0); 
   }
 }
 mmm_26_in = nnn_1_in ;
 }
//lizong_35 <<==--------   --------
 double lizong_36( string uuu_0_st,double uuu_1_do,int uuu_2_in,double uuu_3_do)
 {
  double    nnn_1_do;
  double    nnn_2_do;
  double    nnn_3_do;
  double    nnn_4_do;
  double    nnn_5_do;
  double    nnn_6_do;
  double    nnn_7_do;
  double    nnn_8_do;
  int       nnn_9_in;
  double    nnn_10_do;
//----- -----
 int        ppp_in_1;
 double     ppp_do_2;
 int        ppp_in_3;
 int        ppp_in_4;
 double     ppp_do_5;
 int        ppp_in_6;
 int        ppp_in_7;
 double     ppp_do_8;
 int        ppp_in_9;
 int        ppp_in_10;
 double     ppp_do_11;
 int        ppp_in_12;
 int        ppp_in_13;
 double     ppp_do_14;
 int        ppp_in_15;

 nnn_2_do = SymbolInfoDouble(uuu_0_st,36) ;
 nnn_3_do = SymbolInfoDouble(uuu_0_st,34) ;
 nnn_4_do = SymbolInfoDouble(uuu_0_st,35) ;
 if ( nnn_2_do<0.0001 )
 {
   nnn_2_do = 0.001 ;
 }
 nnn_5_do = 1.0 ;
 nnn_6_do = nnn_3_do ;
 nnn_7_do = 0.0 ;
 if ( GridLevelToStart >  1 && uuu_3_do<0.0099 )
 {
   nnn_7_do = lizong_34(uuu_0_st,false) ;
 }
 if ( GridLevelToStart >  1 && uuu_3_do>0.0099 )
 {
   nnn_7_do = uuu_3_do ;
 }
 if ( GridLevelToStart >  1 )
 {
   if ( uuu_2_in <  GridLevelToStart - 1 )
   {
     ppp_in_1 = uuu_2_in;
     ppp_do_2 = 1.0;
     for (ppp_in_3 = 1 ; ppp_in_3 <= ppp_in_1 ; ppp_in_3=ppp_in_3 + 1)
     {
       if ( ppp_in_3 == 1 )
       {
         ppp_do_2 = TradeMultiplier_2nd;
       }
       if ( ppp_in_3 >= 2 && ppp_in_3 <= 4 )
       {
         ppp_do_2 = ppp_do_2 * TradeMultiplier_3rd;
       }
       if ( ppp_in_3 >= 5 )
       {
         ppp_do_2 = ppp_do_2 * TradeMultiplier_6th;
       }
     }
     nnn_5_do = ppp_do_2 ;
     nnn_6_do = uuu_1_do * nnn_5_do ;
   }
   else
   {
     if ( KeepOriginalProfitLotSize && !(AutoSplit) )
     {
       ppp_in_4 = uuu_2_in;
       ppp_do_5 = 1.0;
       for (ppp_in_6 = 1 ; ppp_in_6 <= ppp_in_4 ; ppp_in_6=ppp_in_6 + 1)
       {
         if ( ppp_in_6 == 1 )
         {
           ppp_do_5 = TradeMultiplier_2nd;
         }
         if ( ppp_in_6 >= 2 && ppp_in_6 <= 4 )
         {
           ppp_do_5 = ppp_do_5 * TradeMultiplier_3rd;
         }
         if ( ppp_in_6 >= 5 )
         {
           ppp_do_5 = ppp_do_5 * TradeMultiplier_6th;
         }
       }
       nnn_5_do = ppp_do_5 ;
       ppp_in_7 = GridLevelToStart - 1;
       ppp_do_8 = 1.0;
       for (ppp_in_9 = 1 ; ppp_in_9 <= ppp_in_7 ; ppp_in_9=ppp_in_9 + 1)
       {
         if ( ppp_in_9 == 1 )
         {
           ppp_do_8 = TradeMultiplier_2nd;
         }
         if ( ppp_in_9 >= 2 && ppp_in_9 <= 4 )
         {
           ppp_do_8 = ppp_do_8 * TradeMultiplier_3rd;
         }
         if ( ppp_in_9 >= 5 )
         {
           ppp_do_8 = ppp_do_8 * TradeMultiplier_6th;
         }
       }
       nnn_8_do = ppp_do_8 ;
       if ( uuu_2_in != GridLevelToStart - 1 )
       {
         nnn_7_do = nnn_7_do / nnn_8_do ;
       }
     }
     else
     {
       ppp_in_10 = uuu_2_in - (GridLevelToStart - 1);
       ppp_do_11 = 1.0;
       for (ppp_in_12 = 1 ; ppp_in_12 <= ppp_in_10 ; ppp_in_12=ppp_in_12 + 1)
       {
         if ( ppp_in_12 == 1 )
         {
           ppp_do_11 = TradeMultiplier_2nd;
         }
         if ( ppp_in_12 >= 2 && ppp_in_12 <= 4 )
         {
           ppp_do_11 = ppp_do_11 * TradeMultiplier_3rd;
         }
         if ( ppp_in_12 >= 5 )
         {
           ppp_do_11 = ppp_do_11 * TradeMultiplier_6th;
         }
       }
       nnn_5_do = ppp_do_11 ;
     }
     nnn_6_do = nnn_7_do * nnn_5_do ;
   }
 }
 else
 {
   ppp_in_13 = uuu_2_in;
   ppp_do_14 = 1.0;
   for (ppp_in_15 = 1 ; ppp_in_15 <= ppp_in_13 ; ppp_in_15=ppp_in_15 + 1)
   {
     if ( ppp_in_15 == 1 )
     {
       ppp_do_14 = TradeMultiplier_2nd;
     }
     if ( ppp_in_15 >= 2 && ppp_in_15 <= 4 )
     {
       ppp_do_14 = ppp_do_14 * TradeMultiplier_3rd;
     }
     if ( ppp_in_15 >= 5 )
     {
       ppp_do_14 = ppp_do_14 * TradeMultiplier_6th;
     }
   }
   nnn_5_do = ppp_do_14 ;
   nnn_6_do = uuu_1_do * nnn_5_do ;
 }
 nnn_9_in = nnn_6_do / nnn_2_do ;
 nnn_6_do = nnn_9_in * nnn_2_do ;
 if ( nnn_6_do<nnn_3_do )
 {
   nnn_6_do = nnn_3_do ;
 }
 if ( nnn_6_do>nnn_4_do && !(AutoSplit) )
 {
   nnn_6_do = nnn_4_do ;
 }
 nnn_10_do = SymbolInfoDouble(uuu_0_st,55) ;
 if ( nnn_6_do>nnn_10_do && nnn_10_do>mmm_25_do )
 {
   nnn_6_do = nnn_10_do ;
 }
 if ( nnn_2_do<0.001001 && nnn_2_do>0.000999 )
 {
   nnn_6_do = NormalizeDouble(nnn_6_do,3) ;
 }
 if ( nnn_2_do<0.010001 && nnn_2_do>0.009999 )
 {
   nnn_6_do = NormalizeDouble(nnn_6_do,2) ;
 }
 if ( nnn_2_do<0.100001 && nnn_2_do>0.099999 )
 {
   nnn_6_do = NormalizeDouble(nnn_6_do,1) ;
 }
 if ( nnn_2_do<1.000001 && nnn_2_do>0.999999 )
 {
   nnn_6_do = NormalizeDouble(nnn_6_do,0) ;
 }
 return(nnn_6_do); 
 }
//lizong_36 <<==--------   --------
 void lizong_37( int uuu_0_in)
 {
  string    nnn_1_st;
  double    nnn_2_do;
  double    nnn_3_do;
  double    nnn_4_do;
  int       nnn_5_in;
  double    nnn_6_do;
  double    nnn_7_do;
  double    nnn_8_do;
  int       nnn_9_in;
  double    nnn_10_do;
  int       nnn_11_in;
  double    nnn_12_do;
  double    nnn_13_do;
  double    nnn_14_do;
  int       nnn_15_in;
  double    nnn_16_do;
  double    nnn_17_do;
  double    nnn_18_do;
  int       nnn_19_in;
  double    nnn_20_do;
  int       nnn_21_in;
  double    nnn_22_do;
//----- -----
 int        ppp_in_1;
 double     ppp_do_2;
 double     ppp_do_3;
 double     ppp_do_4;
 int        ppp_in_5;
 int        ppp_in_6;
 double     ppp_do_7;
 double     ppp_do_8;
 double     ppp_do_9;
 double     ppp_do_10;
 int        ppp_in_11;
 int        ppp_in_12;
 int        ppp_in_13;
 int        ppp_in_14;
 int        ppp_in_15;
 int        ppp_in_16;
 int        ppp_in_17;
 int        ppp_in_18;
 int        ppp_in_19;
 int        ppp_in_20;
 int        ppp_in_21;
 int        ppp_in_22;
 int        ppp_in_23;
 int        ppp_in_24;
 int        ppp_in_25;
 double     ppp_do_26;
 double     ppp_do_27;
 double     ppp_do_28;
 int        ppp_in_29;
 int        ppp_in_30;
 double     ppp_do_31;
 double     ppp_do_32;
 double     ppp_do_33;
 double     ppp_do_34;
 int        ppp_in_35;
 int        ppp_in_36;
 int        ppp_in_37;
 int        ppp_in_38;
 int        ppp_in_39;
 int        ppp_in_40;
 int        ppp_in_41;
 int        ppp_in_42;
 int        ppp_in_43;
 int        ppp_in_44;
 int        ppp_in_45;
 int        ppp_in_46;
 int        ppp_in_47;
 int        ppp_in_48;
 int        ppp_in_49;

 nnn_1_st = gainkit[uuu_0_in].st_1 ;
 CFAE::RefreshRates(); 
 nnn_2_do = CFAE::MarketInfo(nnn_1_st,13) ;
 if ( MaximumTrades - 1 <= 0 || !(TradeMultiplier_3rd>0.0) || !(TradeDistance>mmm_25_do) )   return;
 
 if ( lizong_21(nnn_1_st,0,1) )
 {
   nnn_3_do = lizong_24(nnn_1_st,0,1,false) ;
   nnn_4_do = 0.0 ;
   nnn_5_in = 1 ;
   ppp_in_1=MaximumTrades - 1;
   for ( ; nnn_5_in <= MaximumTrades - 1 ; nnn_5_in ++)
   {
     ppp_in_1=TradeDistance * nnn_5_in;
     nnn_4_do = ppp_in_1 ;
     ppp_do_2 = gainkit[uuu_0_in].do_9 - lizong_22(nnn_1_st,0,1);
     if ( CFAE::MarketInfo(nnn_1_st,11)>mmm_25_do )
     {
       ppp_do_3 = CFAE::MarketInfo(nnn_1_st,11);
     }
     else
     {
       ppp_do_3 = 0.00001;
     }
     ppp_do_4 = ( -(nnn_4_do)) * ppp_do_3;
     ppp_in_5 = 10;
     ppp_in_6 = CFAE::MarketInfo(nnn_1_st,12);
     if ( ppp_in_6 == 5 )
     {
       ppp_in_5 = 10;
     }
     if ( ppp_in_6 == 4 )
     {
       ppp_in_5 = 1;
     }
     if ( ppp_in_6 == 0x3 )
     {
       ppp_in_5 = 10;
     }
     if ( ( ppp_in_6 == 2 || ppp_in_6 == 1 || ppp_in_6 == 0 ) )
     {
       ppp_in_5 = 1;
     }
     if ( !(ppp_do_2<ppp_do_4 * ppp_in_5 * gainkit[uuu_0_in].do_12) || lizong_21(nnn_1_st,nnn_5_in,1) || gainkit[uuu_0_in].bo_10 != 0x0 )   continue;
     nnn_6_do = 0.0 ;
     if ( GridLevelToStart >  1 )
     {
       nnn_6_do = lizong_24(nnn_1_st,GridLevelToStart - 1,1,false) ;
     }
     nnn_7_do = lizong_36(nnn_1_st,nnn_3_do,nnn_5_in,nnn_6_do) ;
     if ( nnn_7_do>0.0 )
     {
       if ( AutoSplit )
       {
         ppp_do_7 = SymbolInfoDouble(nnn_1_st,35);
         ppp_do_8 = SymbolInfoDouble(nnn_1_st,36);
         if ( ppp_do_7>SymbolInfoDouble(nnn_1_st,55) && SymbolInfoDouble(nnn_1_st,55)>mmm_25_do )
         {
           ppp_do_7 = SymbolInfoDouble(nnn_1_st,55);
         }
         if ( ppp_do_8<0.001001 && ppp_do_8>0.000999 )
         {
           ppp_do_7 = NormalizeDouble(ppp_do_7,3);
         }
         if ( ppp_do_8<0.010001 && ppp_do_8>0.009999 )
         {
           ppp_do_7 = NormalizeDouble(ppp_do_7,2);
         }
         if ( ppp_do_8<0.100001 && ppp_do_8>0.099999 )
         {
           ppp_do_7 = NormalizeDouble(ppp_do_7,1);
         }
         if ( ppp_do_8<1.000001 && ppp_do_8>0.999999 )
         {
           ppp_do_7 = NormalizeDouble(ppp_do_7,0);
         }
         nnn_8_do = ppp_do_7 ;
         if ( nnn_7_do>nnn_8_do )
         {
           nnn_9_in = MathCeil(nnn_7_do / nnn_8_do) ;
           nnn_10_do = nnn_7_do ;
           for (nnn_11_in = 0 ; nnn_11_in < nnn_9_in ; nnn_11_in ++)
           {
             nnn_12_do = MathMin(nnn_8_do,nnn_10_do) ;
             ppp_do_9 = nnn_12_do;
             ppp_do_10 = SymbolInfoDouble(nnn_1_st,36);
             if ( ppp_do_10<0.001001 && ppp_do_10>0.000999 )
             {
               ppp_do_9 = NormalizeDouble(ppp_do_9,3);
             }
             if ( ppp_do_10<0.010001 && ppp_do_10>0.009999 )
             {
               ppp_do_9 = NormalizeDouble(ppp_do_9,2);
             }
             if ( ppp_do_10<0.100001 && ppp_do_10>0.099999 )
             {
               ppp_do_9 = NormalizeDouble(ppp_do_9,1);
             }
             if ( ppp_do_10<1.000001 && ppp_do_10>0.999999 )
             {
               ppp_do_9 = NormalizeDouble(ppp_do_9,0);
             }
             nnn_12_do = ppp_do_9 ;
             ppp_in_11 = nnn_5_in;
             if ( nnn_5_in <  0 )
             {
               ppp_in_12 = -1;
             }
             else
             {
               ppp_in_13 = mmm_24_in + UID;
               ppp_in_14 = StringLen(IntegerToString(ppp_in_13,0,32)) ;
               ppp_in_15 = 0;
               if ( 1 == 1 )
               {
                 ppp_in_15 = 1;
               }
               if ( 1 == -1 )
               {
                 ppp_in_15 = 2;
               }
               ppp_in_12 = int(MathPow(10.0,ppp_in_14 + 2)) * ppp_in_15 + ppp_in_13 * 100 + nnn_5_in;
             }
             lizong_42(uuu_0_in,nnn_12_do,ppp_in_12,ppp_in_11); 
             nnn_10_do = nnn_10_do - nnn_12_do ;
             Sleep(500); 
           }
         }
         else
         {
           ppp_in_16 = nnn_5_in;
           if ( nnn_5_in <  0 )
           {
             ppp_in_17 = -1;
           }
           else
           {
             ppp_in_18 = mmm_24_in + UID;
             ppp_in_19 = StringLen(IntegerToString(ppp_in_18,0,32)) ;
             ppp_in_20 = 0;
             if ( 1 == 1 )
             {
               ppp_in_20 = 1;
             }
             if ( 1 == -1 )
             {
               ppp_in_20 = 2;
             }
             ppp_in_17 = int(MathPow(10.0,ppp_in_19 + 2)) * ppp_in_20 + ppp_in_18 * 100 + nnn_5_in;
           }
           lizong_42(uuu_0_in,nnn_7_do,ppp_in_17,ppp_in_16); 
         }
       }
       else
       {
         ppp_in_21 = nnn_5_in;
         if ( nnn_5_in <  0 )
         {
           ppp_in_22 = -1;
         }
         else
         {
           ppp_in_23 = mmm_24_in + UID;
           ppp_in_24 = StringLen(IntegerToString(ppp_in_23,0,32)) ;
           ppp_in_25 = 0;
           if ( 1 == 1 )
           {
             ppp_in_25 = 1;
           }
           if ( 1 == -1 )
           {
             ppp_in_25 = 2;
           }
           ppp_in_22 = int(MathPow(10.0,ppp_in_24 + 2)) * ppp_in_25 + ppp_in_23 * 100 + nnn_5_in;
         }
         lizong_42(uuu_0_in,nnn_7_do,ppp_in_22,ppp_in_21); 
       }
       Sleep(5000); 
     }
     if ( !(lizong_21(nnn_1_st,nnn_5_in,1)) )   continue;
     gainkit[uuu_0_in].bo_10 = true;
     gainkit[uuu_0_in].bo_11 = true;
     
   }
 }
 if ( !(lizong_21(nnn_1_st,0,-1)) )   return;
 nnn_13_do = lizong_24(nnn_1_st,0,-1,false) ;
 nnn_14_do = 0.0 ;
 for (nnn_15_in = 1 ; nnn_15_in <= MaximumTrades - 1 ; nnn_15_in ++)
 {
   nnn_14_do = TradeDistance * nnn_15_in ;
   ppp_do_26 = gainkit[uuu_0_in].do_9 - lizong_22(nnn_1_st,0,-1);
   if ( CFAE::MarketInfo(nnn_1_st,11)>mmm_25_do )
   {
     ppp_do_27 = CFAE::MarketInfo(nnn_1_st,11);
   }
   else
   {
     ppp_do_27 = 0.00001;
   }
   ppp_do_28 = nnn_14_do * ppp_do_27;
   ppp_in_29 = 10;
   ppp_in_30 = CFAE::MarketInfo(nnn_1_st,12);
   if ( ppp_in_30 == 5 )
   {
     ppp_in_29 = 10;
   }
   if ( ppp_in_30 == 4 )
   {
     ppp_in_29 = 1;
   }
   if ( ppp_in_30 == 0x3 )
   {
     ppp_in_29 = 10;
   }
   if ( ( ppp_in_30 == 2 || ppp_in_30 == 1 || ppp_in_30 == 0 ) )
   {
     ppp_in_29 = 1;
   }
   if ( !(ppp_do_26>ppp_do_28 * ppp_in_29 * gainkit[uuu_0_in].do_12) || lizong_21(nnn_1_st,nnn_15_in,-1) || gainkit[uuu_0_in].bo_10 != 0x0 )   continue;
   nnn_16_do = 0.0 ;
   if ( GridLevelToStart >  1 )
   {
     nnn_16_do = lizong_24(nnn_1_st,GridLevelToStart - 1,-1,false) ;
   }
   nnn_17_do = lizong_36(nnn_1_st,nnn_13_do,nnn_15_in,nnn_16_do) ;
   if ( nnn_17_do>0.0 )
   {
     if ( AutoSplit )
     {
       ppp_do_31 = SymbolInfoDouble(nnn_1_st,35);
       ppp_do_32 = SymbolInfoDouble(nnn_1_st,36);
       if ( ppp_do_31>SymbolInfoDouble(nnn_1_st,55) && SymbolInfoDouble(nnn_1_st,55)>mmm_25_do )
       {
         ppp_do_31 = SymbolInfoDouble(nnn_1_st,55);
       }
       if ( ppp_do_32<0.001001 && ppp_do_32>0.000999 )
       {
         ppp_do_31 = NormalizeDouble(ppp_do_31,3);
       }
       if ( ppp_do_32<0.010001 && ppp_do_32>0.009999 )
       {
         ppp_do_31 = NormalizeDouble(ppp_do_31,2);
       }
       if ( ppp_do_32<0.100001 && ppp_do_32>0.099999 )
       {
         ppp_do_31 = NormalizeDouble(ppp_do_31,1);
       }
       if ( ppp_do_32<1.000001 && ppp_do_32>0.999999 )
       {
         ppp_do_31 = NormalizeDouble(ppp_do_31,0);
       }
       nnn_18_do = ppp_do_31 ;
       if ( nnn_17_do>nnn_18_do )
       {
         nnn_19_in = MathCeil(nnn_17_do / nnn_18_do) ;
         nnn_20_do = nnn_17_do ;
         for (nnn_21_in = 0 ; nnn_21_in < nnn_19_in ; nnn_21_in ++)
         {
           nnn_22_do = MathMin(nnn_18_do,nnn_20_do) ;
           ppp_do_33 = nnn_22_do;
           ppp_do_34 = SymbolInfoDouble(nnn_1_st,36);
           if ( ppp_do_34<0.001001 && ppp_do_34>0.000999 )
           {
             ppp_do_33 = NormalizeDouble(ppp_do_33,3);
           }
           if ( ppp_do_34<0.010001 && ppp_do_34>0.009999 )
           {
             ppp_do_33 = NormalizeDouble(ppp_do_33,2);
           }
           if ( ppp_do_34<0.100001 && ppp_do_34>0.099999 )
           {
             ppp_do_33 = NormalizeDouble(ppp_do_33,1);
           }
           if ( ppp_do_34<1.000001 && ppp_do_34>0.999999 )
           {
             ppp_do_33 = NormalizeDouble(ppp_do_33,0);
           }
           nnn_22_do = ppp_do_33 ;
           ppp_in_35 = nnn_15_in;
           if ( nnn_15_in <  0 )
           {
             ppp_in_36 = -1;
           }
           else
           {
             ppp_in_37 = mmm_24_in + UID;
             ppp_in_38 = StringLen(IntegerToString(ppp_in_37,0,32)) ;
             ppp_in_39 = 0;
             if ( -1 == 1 )
             {
               ppp_in_39 = 1;
             }
             if ( -1 == -1 )
             {
               ppp_in_39 = 2;
             }
             ppp_in_36 = int(MathPow(10.0,ppp_in_38 + 2)) * ppp_in_39 + ppp_in_37 * 100 + nnn_15_in;
           }
           lizong_43(uuu_0_in,nnn_22_do,ppp_in_36,ppp_in_35); 
           nnn_20_do = nnn_20_do - nnn_22_do ;
           Sleep(500); 
         }
       }
       else
       {
         ppp_in_40 = nnn_15_in;
         if ( nnn_15_in <  0 )
         {
           ppp_in_41 = -1;
         }
         else
         {
           ppp_in_42 = mmm_24_in + UID;
           ppp_in_43 = StringLen(IntegerToString(ppp_in_42,0,32)) ;
           ppp_in_44 = 0;
           if ( -1 == 1 )
           {
             ppp_in_44 = 1;
           }
           if ( -1 == -1 )
           {
             ppp_in_44 = 2;
           }
           ppp_in_41 = int(MathPow(10.0,ppp_in_43 + 2)) * ppp_in_44 + ppp_in_42 * 100 + nnn_15_in;
         }
         lizong_43(uuu_0_in,nnn_17_do,ppp_in_41,ppp_in_40); 
       }
     }
     else
     {
       ppp_in_45 = nnn_15_in;
       if ( nnn_15_in <  0 )
       {
         ppp_in_46 = -1;
       }
       else
       {
         ppp_in_47 = mmm_24_in + UID;
         ppp_in_48 = StringLen(IntegerToString(ppp_in_47,0,32)) ;
         ppp_in_49 = 0;
         if ( -1 == 1 )
         {
           ppp_in_49 = 1;
         }
         if ( -1 == -1 )
         {
           ppp_in_49 = 2;
         }
         ppp_in_46 = int(MathPow(10.0,ppp_in_48 + 2)) * ppp_in_49 + ppp_in_47 * 100 + nnn_15_in;
       }
       lizong_43(uuu_0_in,nnn_17_do,ppp_in_46,ppp_in_45); 
     }
     Sleep(5000); 
   }
   if ( !(lizong_21(nnn_1_st,nnn_15_in,-1)) )   continue;
   gainkit[uuu_0_in].bo_10 = true;
   gainkit[uuu_0_in].bo_11 = true;
   
 }
 }
//lizong_37 <<==--------   --------
 void lizong_38( int uuu_0_in,long uuu_1_lo,int uuu_2_in,string uuu_3_st,double uuu_4_do,datetime uuu_6_da,double uuu_6_in,double uuu_7_in,double uuu_8_do,double uuu_11_do,int uuu_10_in)
 {
  double    nnn_1_do = 0.0;
  double    nnn_2_do = 0.0;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  double    nnn_6_do;
  double    nnn_7_do;
  double    nnn_8_do;
  double    nnn_9_do;
  double    nnn_10_do;
  int       nnn_11_in;
  double    nnn_12_do;
  int       nnn_13_in;
  double    nnn_14_do;
  int       nnn_15_in;
  double    nnn_16_do;
  double    nnn_17_do;
  double    nnn_18_do;
  bool      nnn_19_bo;
  int       nnn_20_in;
//----- -----
 double     ppp_do_1;
 double     ppp_do_2;
 double     ppp_do_3;
 double     ppp_do_4;
 double     ppp_do_5;

 if ( ( DoNotAdjustTPUnlessNewGrid && TimeCurrent() - gainkit[uuu_0_in].da_27 > 300 ) )   return;
 nnn_3_in=mmm_24_in + UID;
 nnn_4_in=StringLen(IntegerToString(nnn_3_in,0,32)); 
 nnn_5_in=nnn_3_in + int(MathPow(10.0,nnn_4_in));
 nnn_6_do=uuu_6_da - nnn_5_in * 100;
 nnn_7_do = uuu_11_do ;
 nnn_8_do = uuu_11_do ;
 if ( MaximumTrades - 1 >  0 && TradeMultiplier_3rd>0.0 && TradeDistance>mmm_25_do )
 {
   if ( lizong_21(uuu_3_st,0,1) )
   {
     nnn_7_do = NormalizeDouble(lizong_22(uuu_3_st,0,1),CFAE::MarketInfo(uuu_3_st,12)) ;
     gainkit[uuu_0_in].do_23 = nnn_7_do;
   }
   else
   {
     if ( gainkit[uuu_0_in].do_23>mmm_25_do )
     {
       nnn_7_do = gainkit[uuu_0_in].do_23 ;
     }
   }
   nnn_8_do = NormalizeDouble(lizong_23(uuu_3_st,1,true,false),CFAE::MarketInfo(uuu_3_st,12)) ;
   if ( KeepOriginalProfitLotSize && GridLevelToStart >  1 && !(AutoSplit) )
   {
     nnn_8_do = NormalizeDouble(lizong_23(uuu_3_st,1,true,true),CFAE::MarketInfo(uuu_3_st,12)) ;
   }
 }
 nnn_2_do = lizong_40(uuu_0_in,nnn_8_do,1,false,uuu_6_in) ;
 nnn_1_do = lizong_41(uuu_0_in,nnn_7_do,1,false,uuu_7_in,uuu_10_in) ;
 if ( WeightedTP )
 {
   nnn_9_do = nnn_2_do - nnn_8_do ;
   if ( lizong_21(uuu_3_st,0,1) )
   {
     nnn_10_do = lizong_24(uuu_3_st,-1,1,false) ;
     if ( KeepOriginalProfitLotSize && GridLevelToStart >  1 && !(AutoSplit) )
     {
       nnn_10_do = lizong_24(uuu_3_st,-1,1,true) ;
     }
     if ( nnn_10_do>mmm_25_do )
     {
       nnn_11_in = 0 ;
       if ( GridLevelToStart >  1 && !(KeepOriginalProfitLotSize) && lizong_24(uuu_3_st,GridLevelToStart - 1,1,false)>mmm_25_do )
       {
         nnn_11_in=GridLevelToStart - 1;
       }
       nnn_12_do = lizong_24(uuu_3_st,nnn_11_in,1,false) ;
       if ( KeepOriginalProfitLotSize && GridLevelToStart >  1 && !(AutoSplit) )
       {
         nnn_12_do = lizong_24(uuu_3_st,0,1,true) ;
       }
       nnn_12_do = nnn_12_do / nnn_10_do ;
       nnn_9_do = nnn_12_do * nnn_9_do ;
       nnn_2_do = NormalizeDouble(nnn_9_do + nnn_8_do,CFAE::MarketInfo(uuu_3_st,12)) ;
     }
   }
 }
 if ( SmartTP && gainkit[uuu_0_in].do_13>mmm_25_do && lizong_21(uuu_3_st,0,1) && GridLevelToStart == 1 )
 {
   nnn_13_in = 2 ;
   nnn_14_do = InitialTP / 100.0 ;
   if ( !(lizong_21(uuu_3_st,2,1)) )
   {
     nnn_8_do = uuu_11_do ;
     nnn_2_do = nnn_14_do * (nnn_6_do - 2) * gainkit[uuu_0_in].do_13 + uuu_11_do ;
   }
   else
   {
     if ( !(lizong_21(uuu_3_st,nnn_13_in + 3,1)) )
     {
       nnn_2_do = nnn_14_do * gainkit[uuu_0_in].do_13 + nnn_8_do ;
     }
     else
     {
       nnn_2_do = nnn_14_do / 2.0 * gainkit[uuu_0_in].do_13 + nnn_8_do ;
     }
   }
   nnn_2_do = NormalizeDouble(nnn_2_do,CFAE::MarketInfo(uuu_3_st,12)) ;
 }
 if ( lizong_21(uuu_3_st,0,1) )
 {
   gainkit[uuu_0_in].do_25 = nnn_2_do;
 }
 for (nnn_15_in = 0 ; nnn_15_in < 5 ; nnn_15_in ++)
 {
   CFAE::RefreshRates(); 
   nnn_16_do = CFAE::MarketInfo(uuu_3_st,13) ;
   ppp_do_1 = CFAE::MarketInfo(uuu_3_st,14);
   if ( CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do )
   {
     ppp_do_2 = CFAE::MarketInfo(uuu_3_st,11);
   }
   else
   {
     ppp_do_2 = 0.00001;
   }
   nnn_17_do = ppp_do_1 * ppp_do_2 ;
   ppp_do_1 = CFAE::MarketInfo(uuu_3_st,33);
   if ( CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do )
   {
     ppp_do_3 = CFAE::MarketInfo(uuu_3_st,11);
   }
   else
   {
     ppp_do_3 = 0.00001;
   }
   nnn_18_do = ppp_do_1 * ppp_do_3 ;
   if ( nnn_1_do>mmm_25_do )
   {
     if ( nnn_17_do>mmm_25_do && uuu_7_in<mmm_25_do )
     {
       nnn_1_do = MathMin(CFAE::MarketInfo(uuu_3_st,9) - nnn_17_do,nnn_1_do) ;
     }
     if ( nnn_17_do<mmm_25_do )
     {
       nnn_1_do = MathMin(CFAE::MarketInfo(uuu_3_st,9),nnn_1_do) ;
     }
   }
   if ( nnn_2_do>mmm_25_do )
   {
     if ( nnn_17_do>mmm_25_do && uuu_6_in<mmm_25_do )
     {
       nnn_2_do = MathMax(CFAE::MarketInfo(uuu_3_st,9) + nnn_17_do,nnn_2_do) ;
     }
     if ( nnn_17_do<mmm_25_do )
     {
       nnn_2_do = MathMax(CFAE::MarketInfo(uuu_3_st,9),nnn_2_do) ;
     }
   }
   if ( HideSL )
   {
     nnn_1_do = 0.0 ;
   }
   if ( ( HideTP || Use_OPO_Method ) && !(SmartTP) )
   {
     nnn_2_do = 0.0 ;
   }
   nnn_19_bo = true ;
   if ( nnn_2_do<mmm_25_do && !(HideTP) && !(Use_OPO_Method) )
   {
     nnn_19_bo = false ;
   }
   if ( nnn_2_do<mmm_25_do && SmartTP )
   {
     nnn_19_bo = false ;
   }
   if ( nnn_1_do<mmm_25_do && !(HideSL) )
   {
     nnn_19_bo = false ;
   }
   if ( ( !(MathAbs(uuu_6_in - nnn_2_do)>=((CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do) ?CFAE::MarketInfo(uuu_3_st,11):0.00001 ) * 2.0) && !(MathAbs(uuu_7_in - nnn_1_do)>=((CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do) ?CFAE::MarketInfo(uuu_3_st,11):0.00001 ) * 2.0) ) || !(nnn_19_bo) )   continue;
   
   if ( CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do )
   {
     ppp_do_4 = CFAE::MarketInfo(uuu_3_st,11);
   }
   else
   {
     ppp_do_4 = 0.00001;
   }
   if ( MathAbs(uuu_6_in - nnn_2_do)<=ppp_do_4 )
   {
     nnn_2_do = uuu_6_in ;
   }
   if ( CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do )
   {
     ppp_do_5 = CFAE::MarketInfo(uuu_3_st,11);
   }
   else
   {
     ppp_do_5 = 0.00001;
   }
   if ( MathAbs(uuu_7_in - nnn_1_do)<=ppp_do_5 )
   {
     nnn_1_do = uuu_7_in ;
   }
   if ( HideSL )
   {
     nnn_1_do = 0.0 ;
   }
   if ( ( HideTP || Use_OPO_Method ) && !(SmartTP) )
   {
     nnn_2_do = 0.0 ;
   }
   nnn_1_do = NormalizeDouble(nnn_1_do,CFAE::MarketInfo(uuu_3_st,12)) ;
   nnn_2_do = NormalizeDouble(nnn_2_do,CFAE::MarketInfo(uuu_3_st,12)) ;
   if ( lizong_30(uuu_3_st,3,0,uuu_11_do,uuu_7_in,uuu_6_in,uuu_11_do,nnn_1_do,nnn_2_do) )
   {
     Print(TradeComment + " " + uuu_3_st,": Modifying buy trade: " + IntegerToString(uuu_1_lo,0,32) + ", attempt N",IntegerToString(nnn_15_in + 1,0,32)); 
     if ( !(CFAE::OrderModify(uuu_1_lo,uuu_11_do,nnn_1_do,nnn_2_do,0,16711680)) )
     {
       nnn_20_in = CFAE::GetLastError() ;
       Print(TradeComment + " " + uuu_3_st,": Failed to modify buy trade: " + IntegerToString(uuu_1_lo,0,32) + ". Error=",lizong_11(nnn_20_in)); 
       Sleep(5000); 
       if ( ( nnn_20_in != 132 && nnn_20_in != 10018 && nnn_20_in != 4756 ) )   continue;
       Sleep(15000); 
        continue;
     }
     Print(TradeComment + " " + uuu_3_st,": Buy trade: " + IntegerToString(uuu_1_lo,0,32) + " successfully modified"); 
     return;
   }
   Sleep(5000); 
   
 }
 }
//lizong_38 <<==--------   --------
 void lizong_39( int uuu_0_in,long uuu_1_lo,int uuu_2_in,string uuu_3_st,double uuu_4_do,datetime uuu_6_da,double uuu_6_in,double uuu_7_in,double uuu_8_do,double uuu_11_do,int uuu_10_in)
 {
  double    nnn_1_do = 0.0;
  double    nnn_2_do = 0.0;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  double    nnn_6_do;
  double    nnn_7_do;
  double    nnn_8_do;
  double    nnn_9_do;
  double    nnn_10_do;
  int       nnn_11_in;
  double    nnn_12_do;
  int       nnn_13_in;
  double    nnn_14_do;
  int       nnn_15_in;
  double    nnn_16_do;
  double    nnn_17_do;
  double    nnn_18_do;
  bool      nnn_19_bo;
  int       nnn_20_in;
//----- -----
 double     ppp_do_1;
 double     ppp_do_2;
 double     ppp_do_3;
 double     ppp_do_4;
 double     ppp_do_5;

 if ( ( DoNotAdjustTPUnlessNewGrid && TimeCurrent() - gainkit[uuu_0_in].da_28 > 300 ) )   return;
 nnn_3_in=mmm_24_in + UID;
 nnn_4_in=StringLen(IntegerToString(nnn_3_in,0,32)); 
 nnn_5_in=nnn_3_in + int(MathPow(10.0,nnn_4_in)) * 2;
 nnn_6_do=uuu_6_da - nnn_5_in * 100;
 nnn_7_do = uuu_11_do ;
 nnn_8_do = uuu_11_do ;
 if ( MaximumTrades - 1 >  0 && TradeMultiplier_3rd>0.0 && TradeDistance>mmm_25_do )
 {
   if ( lizong_21(uuu_3_st,0,-1) )
   {
     nnn_7_do = NormalizeDouble(lizong_22(uuu_3_st,0,-1),CFAE::MarketInfo(uuu_3_st,12)) ;
     gainkit[uuu_0_in].do_24 = nnn_7_do;
   }
   else
   {
     if ( gainkit[uuu_0_in].do_24>mmm_25_do )
     {
       nnn_7_do = gainkit[uuu_0_in].do_24 ;
     }
   }
   nnn_8_do = NormalizeDouble(lizong_23(uuu_3_st,-1,true,false),CFAE::MarketInfo(uuu_3_st,12)) ;
   if ( KeepOriginalProfitLotSize && GridLevelToStart >  1 && !(AutoSplit) )
   {
     nnn_8_do = NormalizeDouble(lizong_23(uuu_3_st,-1,true,true),CFAE::MarketInfo(uuu_3_st,12)) ;
   }
 }
 nnn_2_do = lizong_40(uuu_0_in,nnn_8_do,-1,false,uuu_6_in) ;
 nnn_1_do = lizong_41(uuu_0_in,nnn_7_do,-1,false,uuu_7_in,uuu_10_in) ;
 if ( WeightedTP )
 {
   nnn_9_do = nnn_8_do - nnn_2_do ;
   if ( lizong_21(uuu_3_st,0,-1) )
   {
     nnn_10_do = lizong_24(uuu_3_st,-1,-1,false) ;
     if ( KeepOriginalProfitLotSize && GridLevelToStart >  1 && !(AutoSplit) )
     {
       nnn_10_do = lizong_24(uuu_3_st,-1,-1,true) ;
     }
     if ( nnn_10_do>mmm_25_do )
     {
       nnn_11_in = 0 ;
       if ( GridLevelToStart >  1 && !(KeepOriginalProfitLotSize) && lizong_24(uuu_3_st,GridLevelToStart - 1,-1,false)>mmm_25_do )
       {
         nnn_11_in=GridLevelToStart - 1;
       }
       nnn_12_do = lizong_24(uuu_3_st,nnn_11_in,-1,false) ;
       if ( KeepOriginalProfitLotSize && GridLevelToStart >  1 && !(AutoSplit) )
       {
         nnn_12_do = lizong_24(uuu_3_st,0,-1,true) ;
       }
       nnn_12_do = nnn_12_do / nnn_10_do ;
       nnn_9_do = nnn_12_do * nnn_9_do ;
       nnn_2_do = NormalizeDouble(nnn_8_do - nnn_9_do,CFAE::MarketInfo(uuu_3_st,12)) ;
     }
   }
 }
 if ( SmartTP && gainkit[uuu_0_in].do_13>mmm_25_do && lizong_21(uuu_3_st,0,-1) && GridLevelToStart == 1 )
 {
   nnn_13_in = 2 ;
   nnn_14_do = InitialTP / 100.0 ;
   if ( !(lizong_21(uuu_3_st,2,-1)) )
   {
     nnn_8_do = uuu_11_do ;
     nnn_2_do = uuu_11_do - nnn_14_do * (nnn_6_do - 2) * gainkit[uuu_0_in].do_13 ;
   }
   else
   {
     if ( !(lizong_21(uuu_3_st,nnn_13_in + 3,-1)) )
     {
       nnn_2_do = nnn_8_do - nnn_14_do * gainkit[uuu_0_in].do_13 ;
     }
     else
     {
       nnn_2_do = nnn_8_do - nnn_14_do / 2.0 * gainkit[uuu_0_in].do_13 ;
     }
   }
   nnn_2_do = NormalizeDouble(nnn_2_do,CFAE::MarketInfo(uuu_3_st,12)) ;
 }
 if ( lizong_21(uuu_3_st,0,-1) )
 {
   gainkit[uuu_0_in].do_26 = nnn_2_do;
 }
 for (nnn_15_in = 0 ; nnn_15_in < 5 ; nnn_15_in ++)
 {
   CFAE::RefreshRates(); 
   nnn_16_do = CFAE::MarketInfo(uuu_3_st,13) ;
   ppp_do_1 = CFAE::MarketInfo(uuu_3_st,14);
   if ( CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do )
   {
     ppp_do_2 = CFAE::MarketInfo(uuu_3_st,11);
   }
   else
   {
     ppp_do_2 = 0.00001;
   }
   nnn_17_do = ppp_do_1 * ppp_do_2 ;
   ppp_do_1 = CFAE::MarketInfo(uuu_3_st,33);
   if ( CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do )
   {
     ppp_do_3 = CFAE::MarketInfo(uuu_3_st,11);
   }
   else
   {
     ppp_do_3 = 0.00001;
   }
   nnn_18_do = ppp_do_1 * ppp_do_3 ;
   if ( nnn_1_do>mmm_25_do )
   {
     if ( nnn_17_do>mmm_25_do && uuu_7_in<mmm_25_do )
     {
       nnn_1_do = MathMax(CFAE::MarketInfo(uuu_3_st,10) + nnn_17_do,nnn_1_do) ;
     }
     if ( nnn_17_do<mmm_25_do )
     {
       nnn_1_do = MathMax(CFAE::MarketInfo(uuu_3_st,10),nnn_1_do) ;
     }
   }
   if ( nnn_2_do>mmm_25_do )
   {
     if ( nnn_17_do>mmm_25_do && uuu_6_in<mmm_25_do )
     {
       nnn_2_do = MathMin(CFAE::MarketInfo(uuu_3_st,10) - nnn_17_do,nnn_2_do) ;
     }
     if ( nnn_17_do<mmm_25_do )
     {
       nnn_2_do = MathMin(CFAE::MarketInfo(uuu_3_st,10),nnn_2_do) ;
     }
   }
   if ( HideSL )
   {
     nnn_1_do = 0.0 ;
   }
   if ( ( HideTP || Use_OPO_Method ) && !(SmartTP) )
   {
     nnn_2_do = 0.0 ;
   }
   nnn_19_bo = true ;
   if ( nnn_2_do<mmm_25_do && !(HideTP) && !(Use_OPO_Method) )
   {
     nnn_19_bo = false ;
   }
   if ( nnn_2_do<mmm_25_do && SmartTP )
   {
     nnn_19_bo = false ;
   }
   if ( nnn_1_do<mmm_25_do && !(HideSL) )
   {
     nnn_19_bo = false ;
   }
   if ( ( !(MathAbs(uuu_6_in - nnn_2_do)>=((CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do) ?CFAE::MarketInfo(uuu_3_st,11):0.00001 ) * 2.0) && !(MathAbs(uuu_7_in - nnn_1_do)>=((CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do) ?CFAE::MarketInfo(uuu_3_st,11):0.00001 ) * 2.0) ) || !(nnn_19_bo) )   continue;
   
   if ( CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do )
   {
     ppp_do_4 = CFAE::MarketInfo(uuu_3_st,11);
   }
   else
   {
     ppp_do_4 = 0.00001;
   }
   if ( MathAbs(uuu_6_in - nnn_2_do)<=ppp_do_4 )
   {
     nnn_2_do = uuu_6_in ;
   }
   if ( CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do )
   {
     ppp_do_5 = CFAE::MarketInfo(uuu_3_st,11);
   }
   else
   {
     ppp_do_5 = 0.00001;
   }
   if ( MathAbs(uuu_7_in - nnn_1_do)<=ppp_do_5 )
   {
     nnn_1_do = uuu_7_in ;
   }
   if ( HideSL )
   {
     nnn_1_do = 0.0 ;
   }
   if ( ( HideTP || Use_OPO_Method ) && !(SmartTP) )
   {
     nnn_2_do = 0.0 ;
   }
   nnn_1_do = NormalizeDouble(nnn_1_do,CFAE::MarketInfo(uuu_3_st,12)) ;
   nnn_2_do = NormalizeDouble(nnn_2_do,CFAE::MarketInfo(uuu_3_st,12)) ;
   if ( lizong_30(uuu_3_st,3,1,uuu_11_do,uuu_7_in,uuu_6_in,uuu_11_do,nnn_1_do,nnn_2_do) )
   {
     Print(TradeComment + " " + uuu_3_st,": Modifying sell trade: " + IntegerToString(uuu_1_lo,0,32) + ", attempt N",IntegerToString(nnn_15_in + 1,0,32)); 
     if ( !(CFAE::OrderModify(uuu_1_lo,uuu_11_do,nnn_1_do,nnn_2_do,0,255)) )
     {
       nnn_20_in = CFAE::GetLastError() ;
       Print(TradeComment + " " + uuu_3_st,": Failed to modify sell trade: " + IntegerToString(uuu_1_lo,0,32) + ". Error=",lizong_11(nnn_20_in)); 
       Sleep(5000); 
       if ( ( nnn_20_in != 132 && nnn_20_in != 10018 && nnn_20_in != 4756 ) )   continue;
       Sleep(15000); 
        continue;
     }
     Print(TradeComment + " " + uuu_3_st,": Sell trade: " + IntegerToString(uuu_1_lo,0,32) + " successfully modified"); 
     return;
   }
   Sleep(5000); 
   
 }
 }
//lizong_39 <<==--------   --------
 double lizong_40( int uuu_0_in,double uuu_1_do,int uuu_2_in,int uuu_3_in,int uuu_4_in)
 {
  double    nnn_1_do;
  string    nnn_2_st;
  double    nnn_3_do;
  double    nnn_4_do;
  double    nnn_5_do;
  int       nnn_6_in;
  double    nnn_7_do;
  double    nnn_8_do;
  double    nnn_9_do;
  double    nnn_10_do;
  double    nnn_11_do;
  double    nnn_12_do;
  double    nnn_13_do;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;

 nnn_2_st = gainkit[uuu_0_in].st_1 ;
 CFAE::RefreshRates(); 
 nnn_3_do = 0.0 ;
 nnn_4_do = 1000.0 ;
 nnn_5_do = 0.0 ;
 ppp_in_1 = 10;
 ppp_in_2 = CFAE::MarketInfo(nnn_2_st,12);
 if ( ppp_in_2 == 5 )
 {
   ppp_in_1 = 10;
 }
 if ( ppp_in_2 == 4 )
 {
   ppp_in_1 = 1;
 }
 if ( ppp_in_2 == 0x3 )
 {
   ppp_in_1 = 10;
 }
 if ( ( ppp_in_2 == 2 || ppp_in_2 == 1 || ppp_in_2 == 0 ) )
 {
   ppp_in_1 = 1;
 }
 nnn_6_in = ppp_in_1 ;
 nnn_7_do = (CFAE::MarketInfo(nnn_2_st,11)>mmm_25_do) ?CFAE::MarketInfo(nnn_2_st,11):0.00001  ;
 nnn_8_do = InitialTP * nnn_7_do * nnn_6_in ;
 if ( nnn_8_do<mmm_25_do )
 {
   nnn_8_do = nnn_4_do * nnn_7_do * nnn_6_in ;
 }
 if ( uuu_2_in == 1 )
 {
   nnn_9_do = 0.0 ;
   if ( !(WeightedTP) )
   {
     nnn_9_do = lizong_24(nnn_2_st,1,1,false) ;
     if ( nnn_9_do>mmm_25_do )
     {
       nnn_8_do = GridTP * nnn_7_do * nnn_6_in ;
     }
   }
   if ( BreakEvenAfterThisLevel >  0 )
   {
     nnn_10_do = lizong_24(nnn_2_st,BreakEvenAfterThisLevel - 1,1,false) ;
     if ( nnn_10_do>mmm_25_do )
     {
       nnn_8_do = 0.0 ;
     }
   }
   nnn_3_do = NormalizeDouble(uuu_1_do + nnn_8_do - nnn_5_do,CFAE::MarketInfo(nnn_2_st,12)) ;
   if ( gainkit[uuu_0_in].do_9>mmm_25_do && nnn_3_do - uuu_1_do>uuu_1_do * 0.5 && nnn_7_do>0.0 )
   {
     nnn_3_do = NormalizeDouble(uuu_1_do + uuu_1_do * 0.5,CFAE::MarketInfo(nnn_2_st,12)) ;
   }
 }
 if ( uuu_2_in == -1 )
 {
   nnn_11_do = 0.0 ;
   if ( !(WeightedTP) )
   {
     nnn_11_do = lizong_24(nnn_2_st,1,-1,false) ;
     if ( nnn_11_do>mmm_25_do )
     {
       nnn_8_do = GridTP * nnn_7_do * nnn_6_in ;
     }
   }
   if ( BreakEvenAfterThisLevel >  0 )
   {
     nnn_12_do = lizong_24(nnn_2_st,BreakEvenAfterThisLevel - 1,-1,false) ;
     if ( nnn_12_do>mmm_25_do )
     {
       nnn_8_do = 0.0 ;
     }
   }
   nnn_3_do = NormalizeDouble(uuu_1_do - nnn_8_do + nnn_5_do,CFAE::MarketInfo(nnn_2_st,12)) ;
   if ( gainkit[uuu_0_in].do_9>mmm_25_do && uuu_1_do - nnn_3_do>uuu_1_do * 0.5 && nnn_7_do>0.0 )
   {
     nnn_3_do = NormalizeDouble(uuu_1_do - uuu_1_do * 0.5,CFAE::MarketInfo(nnn_2_st,12)) ;
   }
 }
 nnn_13_do = SymbolInfoDouble(nnn_2_st,27) ;
 if ( nnn_13_do>0.0 )
 {
   nnn_3_do = MathRound(nnn_3_do / nnn_13_do) * nnn_13_do ;
   nnn_3_do = NormalizeDouble(nnn_3_do,CFAE::MarketInfo(nnn_2_st,12)) ;
 }
 return(nnn_3_do); 
 }
//lizong_40 <<==--------   --------
 double lizong_41( int uuu_0_in,double uuu_1_do,int uuu_2_in,int uuu_3_in,int uuu_4_in,int uuu_5_in)
 {
  double    nnn_1_do;
  string    nnn_2_st;
  double    nnn_3_do;
  double    nnn_4_do;
  int       nnn_5_in;
  double    nnn_6_do;
  double    nnn_7_do;
  double    nnn_8_do;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;

 nnn_2_st = gainkit[uuu_0_in].st_1 ;
 CFAE::RefreshRates(); 
 nnn_3_do = 0.0 ;
 nnn_4_do = 1000.0 ;
 ppp_in_1 = 10;
 ppp_in_2 = CFAE::MarketInfo(nnn_2_st,12);
 if ( ppp_in_2 == 5 )
 {
   ppp_in_1 = 10;
 }
 if ( ppp_in_2 == 4 )
 {
   ppp_in_1 = 1;
 }
 if ( ppp_in_2 == 3 )
 {
   ppp_in_1 = 10;
 }
 if ( ( ppp_in_2 == 2 || ppp_in_2 == 1 || ppp_in_2 == 0 ) )
 {
   ppp_in_1 = 1;
 }
 nnn_5_in = ppp_in_1 ;
 nnn_6_do = (CFAE::MarketInfo(nnn_2_st,11)>mmm_25_do) ?CFAE::MarketInfo(nnn_2_st,11):0.00001  ;
 nnn_7_do = GridSL * nnn_6_do * nnn_5_in ;
 if ( nnn_7_do<mmm_25_do )
 {
   nnn_7_do = nnn_4_do * nnn_6_do * nnn_5_in ;
 }
 if ( uuu_2_in == 1 )
 {
   nnn_3_do = NormalizeDouble(uuu_1_do - nnn_7_do,CFAE::MarketInfo(nnn_2_st,12)) ;
   if ( gainkit[uuu_0_in].do_9>mmm_25_do && uuu_1_do - nnn_3_do>uuu_1_do * 0.5 && nnn_6_do>0.0 )
   {
     nnn_3_do = NormalizeDouble(uuu_1_do - uuu_1_do * 0.5,CFAE::MarketInfo(nnn_2_st,12)) ;
   }
 }
 if ( uuu_2_in == -1 )
 {
   nnn_3_do = NormalizeDouble(uuu_1_do + nnn_7_do,CFAE::MarketInfo(nnn_2_st,12)) ;
   if ( gainkit[uuu_0_in].do_9>mmm_25_do && nnn_3_do - uuu_1_do>uuu_1_do * 0.5 && nnn_6_do>0.0 )
   {
     nnn_3_do = NormalizeDouble(uuu_1_do + uuu_1_do * 0.5,CFAE::MarketInfo(nnn_2_st,12)) ;
   }
 }
 nnn_8_do = SymbolInfoDouble(nnn_2_st,27) ;
 if ( nnn_8_do>0.0 )
 {
   nnn_3_do = MathRound(nnn_3_do / nnn_8_do) * nnn_8_do ;
   nnn_3_do = NormalizeDouble(nnn_3_do,CFAE::MarketInfo(nnn_2_st,12)) ;
 }
 return(nnn_3_do); 
 }
//lizong_41 <<==--------   --------
 void lizong_42( int uuu_0_in,double uuu_1_do,int uuu_2_in,int uuu_3_in)
 {
  string    nnn_1_st;
  double    nnn_2_do;
  double    nnn_3_do;
  long      nnn_5_lo;
  int       nnn_6_in;
//----- -----
 bool       ppp_bo_1;
 int        ppp_in_2;
 int        ppp_in_3;
 int        ppp_in_4;
 double     ppp_do_5;
 int        ppp_in_6;
 string     ppp_st_7;
 string     ppp_st_8;
 double     ppp_do_9;
 double     ppp_do_10;
 int        ppp_in_11;
 int        ppp_in_12;

 nnn_1_st = gainkit[uuu_0_in].st_1 ;
 CFAE::RefreshRates(); 
 nnn_2_do = CFAE::MarketInfo(nnn_1_st,13) ;
 nnn_3_do = CFAE::AccountFreeMarginCheck(nnn_1_st,0,uuu_1_do) ;
 if ( CFAE::IsTesting() )
 {
   ppp_bo_1 = true;
 }
 else
 {
   if ( TerminalInfoInteger(6) == 0 )
   {
     gainkit[uuu_0_in].bo_5 = false;
     gainkit[uuu_0_in].bo_6 = false;
     Print(TradeComment + " " + gainkit[uuu_0_in].st_1,": Signal rejected due to absence of network connection!"); 
     ppp_bo_1 = false;
   }
   else
   {
     ppp_bo_1 = true;
   }
 }
 if ( !(ppp_bo_1) )
 {
   return;
 }
 if ( nnn_3_do<=0.0 )
 {
   Print(TradeComment + " " + nnn_1_st,": Not enough money to send a new averaging buy order: ",DoubleToString(nnn_3_do,2)); 
 }
 else
 {
   Print(TradeComment + " " + nnn_1_st,": Sending a new averaging buy order, attempt N1"); 
   ppp_in_2 = 10;
   ppp_in_3 = CFAE::MarketInfo(nnn_1_st,12);
   if ( ppp_in_3 == 5 )
   {
     ppp_in_2 = 10;
   }
   if ( ppp_in_3 == 4 )
   {
     ppp_in_2 = 1;
   }
   if ( ppp_in_3 == 3 )
   {
     ppp_in_2 = 10;
   }
   if ( ( ppp_in_3 == 2 || ppp_in_3 == 1 || ppp_in_3 == 0 ) )
   {
     ppp_in_2 = 1;
   }
   if ( ( nnn_2_do<MaximumSpread * ppp_in_2 || MaximumSpread<mmm_25_do ) )
   {
     ppp_in_4 = -1;
     ppp_do_5 = 0.0;
     ppp_in_6 = uuu_2_in;
     ppp_st_7 = TradeComment;
     if ( uuu_3_in >  0 )
     {
       ppp_st_7 = TradeComment + " #" + string(uuu_3_in);
     }
     ppp_st_8 = ppp_st_7;
     ppp_do_9 = 0.0;
     ppp_do_10 = 0.0;
     ppp_in_11 = 10;
     ppp_in_12 = CFAE::MarketInfo(nnn_1_st,12);
     if ( ppp_in_12 == 5 )
     {
       ppp_in_11 = 10;
     }
     if ( ppp_in_12 == 4 )
     {
       ppp_in_11 = 1;
     }
     if ( ppp_in_12 == 0x3 )
     {
       ppp_in_11 = 10;
     }
     if ( ( ppp_in_12 == 2 || ppp_in_12 == 1 || ppp_in_12 == 0 ) )
     {
       ppp_in_11 = 1;
     }
     nnn_5_lo = CFAE::OrderSend(nnn_1_st,0,uuu_1_do,CFAE::MarketInfo(nnn_1_st,10),int(MaximumSlippage * ppp_in_11),ppp_do_10,ppp_do_9,ppp_st_8,ppp_in_6,ppp_do_5,ppp_in_4) ;
     if ( nnn_5_lo <  0 )
     {
       nnn_6_in = CFAE::GetLastError() ;
       Print(TradeComment + " " + nnn_1_st,": Failed to send a new averaging sell order. Error:",lizong_11(nnn_6_in)); 
       Sleep(1000); 
     }
     else
     {
       Print(TradeComment + " " + nnn_1_st,": Averaging buy trade is opened, id: ",IntegerToString(nnn_5_lo,0,32)); 
       gainkit[uuu_0_in].da_27 = TimeCurrent();
     }
   }
   else
   {
     Print(TradeComment + " " + nnn_1_st,": Cannot open a new averaging buy trade due to high spread: ",DoubleToString(nnn_2_do,2)); 
     Sleep(5000); 
   }
 }
 }
//lizong_42 <<==--------   --------
 void lizong_43( int uuu_0_in,double uuu_1_do,int uuu_2_in,int uuu_3_in)
 {
  string    nnn_1_st;
  double    nnn_2_do;
  double    nnn_3_do;
  long      nnn_5_lo;
  int       nnn_6_in;
//----- -----
 bool       ppp_bo_1;
 int        ppp_in_2;
 int        ppp_in_3;
 int        ppp_in_4;
 double     ppp_do_5;
 int        ppp_in_6;
 string     ppp_st_7;
 string     ppp_st_8;
 double     ppp_do_9;
 double     ppp_do_10;
 int        ppp_in_11;
 int        ppp_in_12;

 nnn_1_st = gainkit[uuu_0_in].st_1 ;
 CFAE::RefreshRates(); 
 nnn_2_do = CFAE::MarketInfo(nnn_1_st,13) ;
 nnn_3_do = CFAE::AccountFreeMarginCheck(nnn_1_st,1,uuu_1_do) ;
 if ( CFAE::IsTesting() )
 {
   ppp_bo_1 = true;
 }
 else
 {
   if ( TerminalInfoInteger(6) == 0 )
   {
     gainkit[uuu_0_in].bo_5 = false;
     gainkit[uuu_0_in].bo_6 = false;
     Print(TradeComment + " " + gainkit[uuu_0_in].st_1,": Signal rejected due to absence of network connection!"); 
     ppp_bo_1 = false;
   }
   else
   {
     ppp_bo_1 = true;
   }
 }
 if ( !(ppp_bo_1) )
 {
   return;
 }
 if ( nnn_3_do<=0.0 )
 {
   Print(TradeComment + " " + nnn_1_st,": Not enough money to send a new averaging sell order: ",DoubleToString(nnn_3_do,2)); 
 }
 else
 {
   Print(TradeComment + " " + nnn_1_st,": Sending a new averaging sell order, attempt N1"); 
   ppp_in_2 = 10;
   ppp_in_3 = CFAE::MarketInfo(nnn_1_st,12);
   if ( ppp_in_3 == 5 )
   {
     ppp_in_2 = 10;
   }
   if ( ppp_in_3 == 4 )
   {
     ppp_in_2 = 1;
   }
   if ( ppp_in_3 == 3 )
   {
     ppp_in_2 = 10;
   }
   if ( ( ppp_in_3 == 2 || ppp_in_3 == 1 || ppp_in_3 == 0 ) )
   {
     ppp_in_2 = 1;
   }
   if ( ( nnn_2_do<MaximumSpread * ppp_in_2 || MaximumSpread<mmm_25_do ) )
   {
     ppp_in_4 = -1;
     ppp_do_5 = 0.0;
     ppp_in_6 = uuu_2_in;
     ppp_st_7 = TradeComment;
     if ( uuu_3_in >  0 )
     {
       ppp_st_7 = TradeComment + " #" + string(uuu_3_in);
     }
     ppp_st_8 = ppp_st_7;
     ppp_do_9 = 0.0;
     ppp_do_10 = 0.0;
     ppp_in_11 = 10;
     ppp_in_12 = CFAE::MarketInfo(nnn_1_st,12);
     if ( ppp_in_12 == 5 )
     {
       ppp_in_11 = 10;
     }
     if ( ppp_in_12 == 4 )
     {
       ppp_in_11 = 1;
     }
     if ( ppp_in_12 == 0x3 )
     {
       ppp_in_11 = 10;
     }
     if ( ( ppp_in_12 == 2 || ppp_in_12 == 1 || ppp_in_12 == 0 ) )
     {
       ppp_in_11 = 1;
     }
     nnn_5_lo = CFAE::OrderSend(nnn_1_st,1,uuu_1_do,CFAE::MarketInfo(nnn_1_st,9),int(MaximumSlippage * ppp_in_11),ppp_do_10,ppp_do_9,ppp_st_8,ppp_in_6,ppp_do_5,ppp_in_4) ;
     if ( nnn_5_lo <  0 )
     {
       nnn_6_in = CFAE::GetLastError() ;
       Print(TradeComment + " " + nnn_1_st,": Failed to send a new averaging sell order. Error:",lizong_11(nnn_6_in)); 
       Sleep(1000); 
     }
     else
     {
       Print(TradeComment + " " + nnn_1_st,": Averaging sell trade is opened, id: ",IntegerToString(nnn_5_lo,0,32)); 
       gainkit[uuu_0_in].da_28 = TimeCurrent();
     }
   }
   else
   {
     Print(TradeComment + " " + nnn_1_st,": Cannot open a new averaging sell trade due to high spread: ",DoubleToString(nnn_2_do,2)); 
     Sleep(5000); 
   }
 }
 }
//lizong_43 <<==--------   --------
 bool lizong_44( int uuu_0_in,long uuu_1_lo,int uuu_2_in,string uuu_3_st,double uuu_4_do,double uuu_5_do,double uuu_6_do,double uuu_7_do,datetime uuu_9_芼a,double uuu_10_do)
 {
  bool      nnn_1_bo;
  double    nnn_2_do;
  double    nnn_3_do;
  double    nnn_4_do;
  int       nnn_5_in;
  double    nnn_6_do;
  int       nnn_7_in;
  double    nnn_8_do;
  int       nnn_9_in;
  double    nnn_10_do;
  double    nnn_11_do;
  double    nnn_12_do;
  double    nnn_13_do;
  int       nnn_14_in;
  int       nnn_15_in;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;
 int        ppp_in_3;
 int        ppp_in_4;

 CFAE::RefreshRates(); 
 nnn_2_do = CFAE::MarketInfo(uuu_3_st,13) ;
 nnn_3_do = CFAE::MarketInfo(uuu_3_st,10) ;
 nnn_4_do = CFAE::MarketInfo(uuu_3_st,9) ;
 ppp_in_1 = 10;
 ppp_in_2 = CFAE::MarketInfo(uuu_3_st,12);
 if ( ppp_in_2 == 5 )
 {
   ppp_in_1 = 10;
 }
 if ( ppp_in_2 == 4 )
 {
   ppp_in_1 = 1;
 }
 if ( ppp_in_2 == 3 )
 {
   ppp_in_1 = 10;
 }
 if ( ( ppp_in_2 == 2 || ppp_in_2 == 1 || ppp_in_2 == 0 ) )
 {
   ppp_in_1 = 1;
 }
 nnn_5_in = ppp_in_1 ;
 nnn_6_do = (CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do) ?CFAE::MarketInfo(uuu_3_st,11):0.00001  ;
 nnn_7_in = MaximumSlippage * nnn_5_in ;
 nnn_8_do = MaximumSpread * nnn_5_in ;
 nnn_9_in = CFAE::iBarShift(uuu_3_st,mmm_21_in,uuu_9_芼a,true) ;
 gainkit[uuu_0_in].in_15 = nnn_9_in;
 nnn_10_do = 0.0 ;
 nnn_11_do = 999999999.0 ;
 if ( ( HideTP || HideSL || Use_OPO_Method ) )
 {
   nnn_12_do = uuu_10_do ;
   if ( MaximumTrades - 1 >  0 && TradeMultiplier_3rd>0.0 && TradeDistance>mmm_25_do )
   {
     if ( lizong_21(uuu_3_st,0,1) )
     {
       nnn_12_do = NormalizeDouble(lizong_22(uuu_3_st,0,1),CFAE::MarketInfo(uuu_3_st,12)) ;
     }
     else
     {
       if ( gainkit[uuu_0_in].do_23>mmm_25_do )
       {
         nnn_12_do = gainkit[uuu_0_in].do_23 ;
       }
     }
   }
   nnn_10_do = lizong_41(uuu_0_in,nnn_12_do,1,false,uuu_7_do,0) ;
   if ( gainkit[uuu_0_in].do_25>mmm_25_do )
   {
     nnn_11_do = gainkit[uuu_0_in].do_25 ;
   }
 }
 nnn_13_do = gainkit[uuu_0_in].do_9 ;
 if ( OPO_TimeFrame != 15 )
 {
   nnn_13_do = CFAE::iClose(gainkit[uuu_0_in].st_1,OPO_TimeFrame,1) ;
 }
 if ( ( ( nnn_9_in >  gainkit[uuu_0_in].in_14 && gainkit[uuu_0_in].in_14 != 0x0 ) || ( HideSL && nnn_4_do<=nnn_10_do ) || ( HideTP && nnn_4_do>=nnn_11_do && !(Use_OPO_Method) && !(SmartTP) ) || ( Use_OPO_Method && nnn_13_do>=nnn_11_do && !(SmartTP) && gainkit[uuu_0_in].bo_10 == 0x0 && gainkit[uuu_0_in].bo_11 == 0x0 ) || mmm_29_bo ) )
 {
   Print(TradeComment + " " + uuu_3_st,": Closing buy trade: " + IntegerToString(uuu_1_lo,0,32)); 
   if ( HideSL )
   {
     nnn_14_in = 0 ;
     ppp_in_3 = 0;
   }
   if ( ( HideTP || Use_OPO_Method ) && !(SmartTP) )
   {
     nnn_15_in = 0 ;
     ppp_in_4 = 0;
   }
   if ( ( nnn_2_do<nnn_8_do || MaximumSpread<mmm_25_do ) )
   {
     if ( lizong_30(uuu_3_st,1,0,uuu_10_do,uuu_7_do,uuu_6_do,0.0,0.0,0.0) )
     {
       if ( !(CFAE::OrderClose(uuu_1_lo,uuu_4_do,nnn_4_do,nnn_7_in,-1)) )
       {
         Print(TradeComment + " " + uuu_3_st,": Failed to close buy trade: " + IntegerToString(uuu_1_lo,0,32) + ". Error=",lizong_11(CFAE::GetLastError())); 
         return(true); 
       }
       Print(TradeComment + " " + uuu_3_st,": Buy trade: " + IntegerToString(uuu_1_lo,0,32) + " successfully closed"); 
       return(true); 
     }
     Sleep(1000); 
   }
   else
   {
     Print(TradeComment + " " + uuu_3_st,": Cannot close buy trade due to high spread: ",DoubleToString(nnn_2_do,2)); 
     Sleep(1000); 
   }
 }
 return(false); 
 }
//lizong_44 <<==--------   --------
 bool lizong_45( int uuu_0_in,long uuu_1_lo,int uuu_2_in,string uuu_3_st,double uuu_4_do,double uuu_5_do,double uuu_6_do,double uuu_7_do,datetime uuu_9_芼a,double uuu_10_do)
 {
  bool      nnn_1_bo;
  double    nnn_2_do;
  double    nnn_3_do;
  double    nnn_4_do;
  int       nnn_5_in;
  double    nnn_6_do;
  int       nnn_7_in;
  double    nnn_8_do;
  int       nnn_9_in;
  double    nnn_10_do;
  double    nnn_11_do;
  double    nnn_12_do;
  double    nnn_13_do;
  int       nnn_14_in;
  int       nnn_15_in;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;
 int        ppp_in_3;
 int        ppp_in_4;

 CFAE::RefreshRates(); 
 nnn_2_do = CFAE::MarketInfo(uuu_3_st,13) ;
 nnn_3_do = CFAE::MarketInfo(uuu_3_st,10) ;
 nnn_4_do = CFAE::MarketInfo(uuu_3_st,9) ;
 ppp_in_1 = 10;
 ppp_in_2 = CFAE::MarketInfo(uuu_3_st,12);
 if ( ppp_in_2 == 5 )
 {
   ppp_in_1 = 10;
 }
 if ( ppp_in_2 == 4 )
 {
   ppp_in_1 = 1;
 }
 if ( ppp_in_2 == 3 )
 {
   ppp_in_1 = 10;
 }
 if ( ( ppp_in_2 == 2 || ppp_in_2 == 1 || ppp_in_2 == 0 ) )
 {
   ppp_in_1 = 1;
 }
 nnn_5_in = ppp_in_1 ;
 nnn_6_do = (CFAE::MarketInfo(uuu_3_st,11)>mmm_25_do) ?CFAE::MarketInfo(uuu_3_st,11):0.00001  ;
 nnn_7_in = MaximumSlippage * nnn_5_in ;
 nnn_8_do = MaximumSpread * nnn_5_in ;
 nnn_9_in = CFAE::iBarShift(uuu_3_st,mmm_21_in,uuu_9_芼a,true) ;
 gainkit[uuu_0_in].in_15 = nnn_9_in;
 nnn_10_do = 999999999.0 ;
 nnn_11_do = 0.0 ;
 if ( ( HideTP || HideSL || Use_OPO_Method ) )
 {
   nnn_12_do = uuu_10_do ;
   if ( MaximumTrades - 1 >  0 && TradeMultiplier_3rd>0.0 && TradeDistance>mmm_25_do )
   {
     if ( lizong_21(uuu_3_st,0,-1) )
     {
       nnn_12_do = NormalizeDouble(lizong_22(uuu_3_st,0,-1),CFAE::MarketInfo(uuu_3_st,12)) ;
     }
     else
     {
       if ( gainkit[uuu_0_in].do_24>mmm_25_do )
       {
         nnn_12_do = gainkit[uuu_0_in].do_24 ;
       }
     }
   }
   nnn_10_do = lizong_41(uuu_0_in,nnn_12_do,-1,false,uuu_7_do,0) ;
   if ( gainkit[uuu_0_in].do_26>mmm_25_do )
   {
     nnn_11_do = gainkit[uuu_0_in].do_26 ;
   }
 }
 nnn_13_do = gainkit[uuu_0_in].do_9 ;
 if ( OPO_TimeFrame != 15 )
 {
   nnn_13_do = CFAE::iClose(gainkit[uuu_0_in].st_1,OPO_TimeFrame,1) ;
 }
 if ( ( ( nnn_9_in >  gainkit[uuu_0_in].in_14 && gainkit[uuu_0_in].in_14 != 0x0 ) || ( HideSL && nnn_3_do>=nnn_10_do ) || ( HideTP && nnn_3_do<=nnn_11_do && !(Use_OPO_Method) && !(SmartTP) ) || ( Use_OPO_Method && nnn_3_do - nnn_4_do + nnn_13_do<=nnn_11_do && !(SmartTP) && gainkit[uuu_0_in].bo_10 == 0x0 && gainkit[uuu_0_in].bo_11 == 0x0 ) || mmm_29_bo ) )
 {
   Print(TradeComment + " " + uuu_3_st,": Closing sell trade: " + IntegerToString(uuu_1_lo,0,32)); 
   if ( HideSL )
   {
     nnn_14_in = 0 ;
     ppp_in_3 = 0;
   }
   if ( ( HideTP || Use_OPO_Method ) && !(SmartTP) )
   {
     nnn_15_in = 0 ;
     ppp_in_4 = 0;
   }
   if ( ( nnn_2_do<nnn_8_do || MaximumSpread<mmm_25_do ) )
   {
     if ( lizong_30(uuu_3_st,1,1,uuu_10_do,uuu_7_do,uuu_6_do,0.0,0.0,0.0) )
     {
       if ( !(CFAE::OrderClose(uuu_1_lo,uuu_4_do,nnn_3_do,nnn_7_in,-1)) )
       {
         Print(TradeComment + " " + uuu_3_st,": Failed to close sell trade: " + IntegerToString(uuu_1_lo,0,32) + ". Error=",lizong_11(CFAE::GetLastError())); 
         return(true); 
       }
       Print(TradeComment + " " + uuu_3_st,": Sell trade: " + IntegerToString(uuu_1_lo,0,32) + " successfully closed"); 
       return(true); 
     }
     Sleep(1000); 
   }
   else
   {
     Print(TradeComment + " " + uuu_3_st,": Cannot close sell trade due to high spread: ",DoubleToString(nnn_2_do,2)); 
     Sleep(1000); 
   }
 }
 return(false); 
 }
//lizong_45 <<==--------   --------
 void lizong_46()
 {
  string    nnn_1_st;
  int       nnn_2_in;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  int       nnn_6_in;
  int       nnn_7_in;
  bool      nnn_8_bo;
  bool      nnn_9_bo;
  bool      nnn_10_bo;
  int       nnn_11_in;
  int       nnn_12_in;
//----- -----

 nnn_1_st = "R_Label" ;
 nnn_2_in = 2960685 ;
 nnn_3_in = 1 ;
 nnn_4_in = 0 ;
 nnn_5_in = 8388608 ;
 nnn_6_in = 0 ;
 nnn_7_in = 2 ;
 nnn_8_bo = false ;
 nnn_9_bo = false ;
 nnn_10_bo = true ;
 nnn_12_in = 0 ;
 nnn_11_in = 0 ;
 ResetLastError();
 if ( CFAE::ObjectFind(0,nnn_1_st) == -1 )
 {
   if ( !(mmm_10_a_167.CreateBitmap(0,0,"R_Label",5,17,100,100)) )
   {
     Print("Error creating canvas: ",CFAE::GetLastError()); 
   }
   else
   {
     mmm_10_a_167.CCanvasX_12("::W2.12LD_bmp\\WakaWakaEA.bmp"); 
     mmm_10_a_167.TransparentLevelSet(210);
     mmm_10_a_167.Update(0);
   }
 }
 ChartRedraw(0); 
 Sleep(500); 
 }
//lizong_46 <<==--------   --------
 void lizong_47( string uuu_0_st,int uuu_1_in)
 {
  bool      nnn_1_bo = false;
  bool      nnn_2_bo = false;
  int       nnn_3_in;
  int       nnn_4_in;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;

 if ( uuu_1_in == -1 )
 {
   nnn_2_bo = true ;
 }
 if ( uuu_1_in == 1 )
 {
   nnn_1_bo = true ;
 }
 if ( CFAE::AccountFreeMargin()<10.0 )
 {
   nnn_1_bo = false ;
   nnn_2_bo = false ;
   Print(TradeComment + " " + uuu_0_st,": Not enough money: ",DoubleToString(MathFloor(CFAE::AccountFreeMargin()),2)); 
 }
 if ( ( UID > 9 || UID <  0 ) )
 {
   Print(TradeComment + " " + uuu_0_st,": UID value issue!"); 
   nnn_1_bo = false ;
   nnn_2_bo = false ;
 }
 nnn_3_in = SymbolInfoInteger(uuu_0_st,30) ;
 switch(nnn_3_in)
 {
   case 0 :
   Print(TradeComment + " " + uuu_0_st,": Trading is disabled for ",uuu_0_st); 
   nnn_1_bo = false ;
   nnn_2_bo = false ;
     break;
   case 3 :
   nnn_1_bo = false ;
   nnn_2_bo = false ;
     break;
   case 4 :
   nnn_1_bo = false ;
   nnn_2_bo = false ;
     break;
   case 1 :
   nnn_1_bo = false ;
   nnn_2_bo = false ;
 }
 ppp_in_1 = 0;
 for (ppp_in_2 = 0 ; ppp_in_2 < ArraySize(gainkit) ; ppp_in_2=ppp_in_2 + 1)
 {
   if ( lizong_21(gainkit[ppp_in_2].st_1,0,0) )
   {
     ppp_in_1=ppp_in_1 + 1;
   }
 }
 if ( ppp_in_1 >= MaximumSymbols )
 {
   nnn_1_bo = false ;
   nnn_2_bo = false ;
 }
 for (nnn_4_in = 0 ; nnn_4_in < ArraySize(gainkit) ; nnn_4_in ++)
 {
   if ( gainkit[nnn_4_in].st_1 == uuu_0_st )
   {
     gainkit[nnn_4_in].bo_5 = nnn_1_bo;
     gainkit[nnn_4_in].bo_6 = nnn_2_bo;
     lizong_33(nnn_4_in,true); 
     gainkit[nnn_4_in].bo_5 = false;
     gainkit[nnn_4_in].bo_6 = false;
     return;
   }
 }
 }
//lizong_47 <<==--------   --------
 void lizong_48( string uuu_0_st)
 {
  int       nnn_1_in;
//----- -----
 int        ppp_in_1;
 int        ppp_in_2;

 if ( uuu_0_st == "but_Suspend" && CFAE::ObjectFind(0,"but_Suspend") != -1 )
 {
   mmm_37_bo=!(CFAE::ObjectGetInteger(0,"but_Suspend",OBJPROP_STATE,0));
   if ( CFAE::ObjectGetInteger(0,"but_Suspend",OBJPROP_STATE,0) == 0 )
   {
     CFAE::ObjectSetInteger(0,"but_Suspend",OBJPROP_BGCOLOR,32768); 
     CFAE::ObjectSetString(0,"but_Suspend",OBJPROP_TEXT,"New grids allowed"); 
   }
   if ( !(mmm_37_bo) )
   {
     CFAE::ObjectSetInteger(0,"but_Suspend",OBJPROP_BGCOLOR,255); 
     CFAE::ObjectSetString(0,"but_Suspend",OBJPROP_TEXT,"New grids NOT allowed!"); 
     for (ppp_in_1 = 0 ; ppp_in_1 < ArraySize(gainkit) ; ppp_in_1=ppp_in_1 + 1)
     {
       gainkit[ppp_in_1].bo_5 = false;
       gainkit[ppp_in_1].bo_6 = false;
     }
   }
   ChartRedraw(0); 
 }
 if ( uuu_0_st == "but_Buy" && CFAE::ObjectFind(0,"but_Buy") != -1 )
 {
   Sleep(100); 
   CFAE::ObjectSetInteger(0,"but_Buy",OBJPROP_STATE,0); 
   ChartRedraw(0); 
   lizong_47(mmm_36_st,1); 
 }
 if ( uuu_0_st == "but_Sell" && CFAE::ObjectFind(0,"but_Sell") != -1 )
 {
   Sleep(100); 
   CFAE::ObjectSetInteger(0,"but_Sell",OBJPROP_STATE,0); 
   ChartRedraw(0); 
   lizong_47(mmm_36_st,-1); 
 }
 if ( uuu_0_st != "but_Pair" || CFAE::ObjectFind(0,"but_Pair") == -1 )   return;
 Sleep(100); 
 CFAE::ObjectSetInteger(0,"but_Pair",OBJPROP_STATE,0); 
 if ( mmm_36_st == "Select pair" )
 {
   mmm_36_st = gainkit[0].st_1 ;
 }
 else
 {
   for (nnn_1_in = 0 ; nnn_1_in < ArraySize(gainkit) ; nnn_1_in ++)
   {
     if ( gainkit[nnn_1_in].st_1 == mmm_36_st && nnn_1_in <  ArraySize(gainkit) - 1 )
     {
       mmm_36_st = gainkit[nnn_1_in + 1].st_1 ;
       break;
     }
     if ( gainkit[nnn_1_in].st_1 != mmm_36_st )   continue;
     ppp_in_2=ArraySize(gainkit) - 1;
     if ( nnn_1_in != ppp_in_2 )   continue;
     mmm_36_st = "Select pair" ;
     break;
     
   }
 }
 CFAE::ObjectSetString(0,"but_Pair",OBJPROP_TEXT,mmm_36_st); 
 ChartRedraw(0); 
 }
//lizong_48 <<==--------   --------
 void lizong_49( bool uuu_0_bo)
 {
  int       nnn_1_in;
  int       nnn_2_in;
  int       nnn_3_in;
  int       nnn_4_in;
  int       nnn_5_in;
  int       nnn_6_in;
  int       nnn_7_in;
  string    nnn_8_st;
  int       nnn_9_in;
  int       nnn_10_in;
  string    nnn_11_st;
  string    nnn_12_st;
  double    nnn_13_do;
  int       nnn_14_in;
  double    nnn_15_do;
  int       nnn_16_in;
  int       nnn_17_in;
  string    nnn_18_st;
//----- -----
 int        ppp_in_1;
 double     ppp_do_2;
 int        ppp_in_3;
 int        ppp_in_4;
 int        ppp_in_5;
 int        ppp_in_6;
 string     ppp_st_7;
 int        ppp_in_8;
 bool       ppp_bo_9;

 nnn_1_in = 16777215 ;
 nnn_2_in = 14474460 ;
 ppp_in_1 = TerminalInfoInteger(8);
 if ( ppp_in_1 != 0 )
 {
   ppp_in_1 = AccountInfoInteger(ACCOUNT_TRADE_EXPERT);
 }
 if ( ppp_in_1 != 0 )
 {
   ppp_in_1 = MQLInfoInteger(MQL_TRADE_ALLOWED);
 }
 if ( ( ppp_in_1 == 0 || mmm_35_bo ) )
 {
   nnn_1_in = 4678655 ;
   nnn_2_in = 4678655 ;
 }
 nnn_3_in = 0 ;
 nnn_4_in = 23 ;
 nnn_5_in = 15 ;
 nnn_6_in = 14 ;
 nnn_7_in = 100 ;
 nnn_8_st = "MS Sans Serif" ;
 nnn_9_in = 6 ;
 nnn_10_in = 205 ;
 if ( CFAE::ObjectFind(0,"but_Buy") == -1 )
 {
   lizong_50(0,"but_Buy",0,10,205,40,20,0,"Buy",nnn_8_st,6,16777215,25600,25600,false,false,false,true,0); 
 }
 if ( CFAE::ObjectFind(0,"but_Sell") == -1 )
 {
   lizong_50(0,"but_Sell",0,125,nnn_10_in,40,20,0,"Sell",nnn_8_st,nnn_9_in,16777215,139,139,false,false,false,true,0); 
 }
 if ( CFAE::ObjectFind(0,"but_Pair") == -1 )
 {
   lizong_50(0,"but_Pair",0,52,nnn_10_in,71,20,0,mmm_36_st,nnn_8_st,nnn_9_in,16777215,2139610,2139610,false,false,false,true,0); 
 }
 if ( CFAE::ObjectFind(0,"but_Suspend") == -1 )
 {
   lizong_50(0,"but_Suspend",0,10,162,155,20,0,"New grids allowed",nnn_8_st,nnn_9_in,16777215,32768,32768,false,false,false,true,0); 
 }
 if ( CFAE::ObjectFind(0,"but_Suspend") != -1 )
 {
   mmm_37_bo=!(CFAE::ObjectGetInteger(0,"but_Suspend",OBJPROP_STATE,0));
   if ( CFAE::ObjectGetInteger(0,"but_Suspend",OBJPROP_STATE,0) == 0 )
   {
     CFAE::ObjectSetInteger(0,"but_Suspend",OBJPROP_BGCOLOR,32768); 
     CFAE::ObjectSetString(0,"but_Suspend",OBJPROP_TEXT,"New grids allowed"); 
   }
   if ( !(mmm_37_bo) )
   {
     CFAE::ObjectSetInteger(0,"but_Suspend",OBJPROP_BGCOLOR,255); 
     CFAE::ObjectSetString(0,"but_Suspend",OBJPROP_TEXT,"New grids NOT allowed!"); 
     for (ppp_in_1 = 0 ; ppp_in_1 < ArraySize(gainkit) ; ppp_in_1=ppp_in_1 + 1)
     {
       gainkit[ppp_in_1].bo_5 = false;
       gainkit[ppp_in_1].bo_6 = false;
     }
   }
   ChartRedraw(0); 
 }
 nnn_4_in +=30;
 nnn_11_st = "-----" ;
 if ( ( !(uuu_0_bo) || CFAE::IsTesting() ) )
 {
   nnn_11_st = DoubleToString(lizong_34(gainkit[0].st_1,false),2) ;
 }
 lizong_31("GraphicsC" + string(nnn_4_in),nnn_3_in,nnn_5_in,nnn_4_in,"Start lot:",nnn_8_st,nnn_2_in,nnn_9_in); 
 lizong_31("GraphicsV" + string(nnn_4_in),nnn_3_in,nnn_7_in,nnn_4_in,nnn_11_st,nnn_8_st,nnn_1_in,nnn_9_in); 
 nnn_4_in +=nnn_6_in;
 lizong_31("GraphicsC" + string(nnn_4_in),nnn_3_in,nnn_5_in,nnn_4_in,"Currencies:",nnn_8_st,nnn_2_in,nnn_9_in); 
 lizong_31("GraphicsV" + string(nnn_4_in),nnn_3_in,nnn_7_in,nnn_4_in,string(ArraySize(gainkit)),nnn_8_st,nnn_1_in,nnn_9_in); 
 nnn_4_in +=nnn_6_in;
 lizong_31("GraphicsC" + string(nnn_4_in),nnn_3_in,nnn_5_in,nnn_4_in,"Leverage:",nnn_8_st,nnn_2_in,nnn_9_in); 
 lizong_31("GraphicsV" + string(nnn_4_in),nnn_3_in,nnn_7_in,nnn_4_in,"1:" + AccountInfoInteger(ACCOUNT_LEVERAGE),nnn_8_st,nnn_1_in,nnn_9_in); 
 nnn_4_in +=nnn_6_in;
 nnn_12_st = TradeComment ;
 if ( StringLen(TradeComment)  >  9.881312916825e-323 )
 {
   nnn_12_st = CFAE::StringSubstr(TradeComment,0,20) ;
 }
 nnn_13_do = 0.0 ;
 for (nnn_14_in = 0 ; nnn_14_in < ArraySize(gainkit) ; nnn_14_in ++)
 {
   nnn_13_do = nnn_13_do + lizong_24(gainkit[nnn_14_in].st_1,-1,0,false) ;
 }
 lizong_31("GraphicsC" + string(nnn_4_in),nnn_3_in,nnn_5_in,nnn_4_in,"Lots opened:",nnn_8_st,nnn_2_in,nnn_9_in); 
 lizong_31("GraphicsV" + string(nnn_4_in),nnn_3_in,nnn_7_in,nnn_4_in,DoubleToString(nnn_13_do,3),nnn_8_st,nnn_1_in,nnn_9_in); 
 nnn_4_in +=nnn_6_in;
 ppp_do_2 = 0.0;
 ppp_in_3 = mmm_24_in + UID + int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32)) ));
 ppp_in_4 = mmm_24_in + UID + int(MathPow(10.0,StringLen(IntegerToString(mmm_24_in + UID,0,32)) )) * 2;
 for (ppp_in_5 = 0 ; ppp_in_5 < CFAE::OrdersTotal() ; ppp_in_5=ppp_in_5 + 1)
 {
   if ( CFAE::OrderSelect(ppp_in_5,0,0) )
   {
     ppp_in_6 = CFAE::OrderType();
     CFAE::OrderSymbol(); 
     ppp_in_8 = CFAE::OrderMagicNumber() / 100;
     if ( ( ( ppp_in_6 != 0 || ppp_in_3 != ppp_in_8 ) && (ppp_in_6 != 1 || ppp_in_4 != ppp_in_8) ) )   continue;
     ppp_do_2 = CFAE::OrderProfit() + CFAE::OrderSwap() + CFAE::OrderCommission() + ppp_do_2;
      continue;
   }
   Print(TradeComment + " " + "------",": Failed to select an order! Error=",lizong_11(CFAE::GetLastError())); 
   
 }
 nnn_15_do = ppp_do_2 ;
 lizong_31("GraphicsC" + string(nnn_4_in),nnn_3_in,nnn_5_in,nnn_4_in,"Floating PnL:",nnn_8_st,nnn_2_in,nnn_9_in); 
 nnn_16_in = nnn_1_in ;
 if ( nnn_15_do<0.0 )
 {
   nnn_16_in = 4678655 ;
 }
 lizong_31("GraphicsV" + string(nnn_4_in),nnn_3_in,nnn_7_in,nnn_4_in,DoubleToString(nnn_15_do,2),nnn_8_st,nnn_16_in,nnn_9_in); 
 nnn_4_in +=nnn_6_in;
 lizong_31("GraphicsC" + string(nnn_4_in),nnn_3_in,nnn_5_in,nnn_4_in,"Comment:",nnn_8_st,nnn_2_in,nnn_9_in); 
 lizong_31("GraphicsV" + string(nnn_4_in),nnn_3_in,nnn_7_in,nnn_4_in,nnn_12_st,nnn_8_st,nnn_1_in,nnn_9_in); 
 nnn_4_in +=nnn_6_in;
 nnn_4_in +=8;
 nnn_17_in = 16495626 ;
 nnn_18_st = "Live trading" ;
 ppp_bo_9 = TerminalInfoInteger(8);
 if ( ppp_bo_9 )
 {
   ppp_bo_9 = AccountInfoInteger(ACCOUNT_TRADE_EXPERT);
 }
 if ( ppp_bo_9 )
 {
   ppp_bo_9 = MQLInfoInteger(MQL_TRADE_ALLOWED);
 }
 if ( !(ppp_bo_9) )
 {
   nnn_18_st = "Trading not allowed!" ;
   nnn_17_in = 4678655 ;
 }
 if ( !(AllowOpeningNewGrid) )
 {
   nnn_18_st = "New grids NOT allowed!" ;
   nnn_17_in = 4678655 ;
 }
 if ( TerminalInfoInteger(8) == 0 )
 {
   nnn_18_st = "Terminal: trading not allowed!" ;
   nnn_17_in = 4678655 ;
 }
 if ( AccountInfoInteger(ACCOUNT_TRADE_EXPERT) == 0 )
 {
   nnn_18_st = "Account: trading not allowed!" ;
   nnn_17_in = 4678655 ;
 }
 if ( MQLInfoInteger(MQL_TRADE_ALLOWED) == 0 )
 {
   nnn_18_st = "MQL: trading not allowed!" ;
   nnn_17_in = 4678655 ;
 }
 if ( Period() != 15 )
 {
   nnn_18_st = "M15 is needed!" ;
   nnn_17_in = 4678655 ;
 }
 if ( mmm_35_bo )
 {
   nnn_18_st = "Check Symbols!" ;
   nnn_17_in = 4678655 ;
 }
 if ( CFAE::IsVisualMode() )
 {
   nnn_18_st = "Backtesting" ;
 }
 lizong_31("GraphicsC" + string(nnn_4_in),nnn_3_in,nnn_5_in,nnn_4_in,nnn_18_st,nnn_8_st,nnn_17_in,nnn_9_in); 
 nnn_4_in +=160;
 lizong_31("GraphicsC" + string(nnn_4_in),nnn_3_in,nnn_5_in,nnn_4_in,"v" + mmm_2_st,nnn_8_st,nnn_2_in,nnn_9_in); 
 }
//lizong_49 <<==--------   --------
 bool lizong_50( long uuu_0_lo,string uuu_1_st,int uuu_2_in,int uuu_3_in,int uuu_4_in,int uuu_5_in,int uuu_6_in,int uuu_7_in,string uuu_8_st,string uuu_9_st,int uuu_10_in,int uuu_11_in,int uuu_12_in,int uuu_13_in,char uuu_14_ch,char uuu_15_ch,char uuu_16_ch,char uuu_17_ch,long uuu_18_lo)
 {
  bool      nnn_1_bo;
//----- -----

 ResetLastError();
 if ( !(CFAE::ObjectCreate(uuu_0_lo,uuu_1_st,25,uuu_2_in,0,0.0)) )
 {
   Print("Error creating canvas: ",lizong_11(CFAE::GetLastError())); 
   return(false); 
 }
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_XDISTANCE,uuu_3_in); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_YDISTANCE,uuu_4_in); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_XSIZE,uuu_5_in); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_YSIZE,uuu_6_in); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_CORNER,uuu_7_in); 
 CFAE::ObjectSetString(uuu_0_lo,uuu_1_st,OBJPROP_TEXT,uuu_8_st); 
 CFAE::ObjectSetString(uuu_0_lo,uuu_1_st,OBJPROP_FONT,uuu_9_st); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_FONTSIZE,uuu_10_in); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_COLOR,uuu_11_in); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_BGCOLOR,uuu_12_in); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_BORDER_COLOR,uuu_13_in); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_BACK,uuu_15_ch); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_STATE,uuu_14_ch); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_SELECTABLE,uuu_16_ch); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_SELECTED,uuu_16_ch); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_HIDDEN,uuu_17_ch); 
 CFAE::ObjectSetInteger(uuu_0_lo,uuu_1_st,OBJPROP_ZORDER,uuu_18_lo); 
 return(true); 
 }
//<<==lizong_50 <<==



//== WAKA MQL5 ==//

//-- Global Variables
int FXD_SELECTED_TYPE = 0;// Indicates what is selected by OrderSelect, 1 for trade, 2 for pending order, 3 for history trade
ulong FXD_SELECTED_TICKET = 0;// The ticket number selected by OrderSelect
int FXD_INDICATOR_COUNTED_MEMORY = 0;// Used as a memory for IndicatorCounted() function. It needs to be outside of the function, because when OnCalculate needs to be reset, this memory must be reset as well.

// Set the missing predefined variables, which are controlled by RefreshRates
int Bars     = Bars(_Symbol, PERIOD_CURRENT);
int Digits   = _Digits;
double Point = _Point;
double Ask, Bid, Close[], High[], Low[], Open[];
long Volume[];
datetime Time[];

void OnTick()
{
	CFAE::RefreshRates();
	__OnTick__();
}



class CFAE
{
private:
	/**
	* _LastError is used to set custom errors that could be returned by the custom GetLastError method
	* The initial value should be -1 and everything >= 0 should be valid error code
	* When setting an error code in it, it should be the MQL5 value,
	* because then in GetLastError it will be converted to MQL4 value
	*/
	static int _LastError;
public:
	CFAE() {
		
	};
	
	static double AccountFreeMargin() {
		return ::AccountInfoDouble(ACCOUNT_MARGIN_FREE);
	}
	
	static double  AccountFreeMarginCheck(string symbol, int cmd, double volume) {
		MqlTick last_tick;
	
		if (::SymbolInfoTick(symbol, last_tick)) {
			double freeMargin = ::AccountInfoDouble(ACCOUNT_MARGIN_FREE);
			double margin = 0.0;
	
			if (::OrderCalcMargin((ENUM_ORDER_TYPE)cmd, symbol, volume, ((cmd==0) ? last_tick.ask : last_tick.bid), margin)) {
				return (freeMargin - margin);
			}
		}
	
		return 0;
	}
	
	/**
	* In MQL4's documentation errors are also shown as numeric values and sometimes people use these numbers, because they are shorter to write.
	* This means that GetLastError shoud return such MQL4 numeric values instead of the MQL5 values.
	* Supports custom error codes that can be set with CFAE -> _LastError
	*/
	static int GetLastError() {
		int errorCode = 0;
	
		if (CFAE::_LastError >= 0) {
			errorCode = CFAE::_LastError;
			CFAE::_LastError = -1;
		}
		else {
			errorCode = ::GetLastError();
		}
	
		switch (errorCode) {
			//--- errors returned from trade server
			case ERR_SUCCESS                       : return 0; /* ERR_NO_ERROR */
			//case ERR_NO_RESULT                   : return 1; /* ERR_NO_RESULT */
			//case ERR_COMMON_ERROR                : return 2; /* ERR_COMMON_ERROR */
			case TRADE_RETCODE_INVALID             : return 3; /* ERR_INVALID_TRADE_PARAMETERS */
			case ERR_TRADE_SEND_FAILED             : return 4; /* ERR_SERVER_BUSY */
			//case ERR_OLD_VERSION                 : return 5; /* ERR_OLD_VERSION */
			case TRADE_RETCODE_CONNECTION          : return 6; /* ERR_NO_CONNECTION */
			case TRADE_RETCODE_REJECT              : return 7; /* ERR_NOT_ENOUGH_RIGHTS */
			//case TRADE_RETCODE_TOO_MANY_REQUESTS : return 8; /* ERR_TOO_FREQUENT_REQUESTS */
			case TRADE_RETCODE_ERROR               : return 9; /* ERR_MALFUNCTIONAL_TRADE */
			//case ERR_ACCOUNT_DISABLED            : return 64; /* ERR_ACCOUNT_DISABLED */
			//case ERR_INVALID_ACCOUNT             : return 65; /* ERR_INVALID_ACCOUNT */
			case TRADE_RETCODE_TIMEOUT             : return 128; /* ERR_TRADE_TIMEOUT */
			case TRADE_RETCODE_INVALID_PRICE       : return 129; /* ERR_INVALID_PRICE */
			case TRADE_RETCODE_INVALID_STOPS       : return 130; /* ERR_INVALID_STOPS */
			case TRADE_RETCODE_INVALID_VOLUME      : return 131; /* ERR_INVALID_TRADE_VOLUME */
			case TRADE_RETCODE_MARKET_CLOSED       : return 132; /* ERR_MARKET_CLOSED */
			case TRADE_RETCODE_TRADE_DISABLED      : return 133; /* ERR_TRADE_DISABLED */
			case TRADE_RETCODE_NO_MONEY            : return 134; /* ERR_NOT_ENOUGH_MONEY */
			case TRADE_RETCODE_PRICE_CHANGED       : return 135; /* ERR_PRICE_CHANGED */
			case TRADE_RETCODE_PRICE_OFF           : return 136; /* ERR_OFF_QUOTES */
			//case ERR_TRADE_SEND_FAILED           : return 137; /* ERR_BROKER_BUSY */
			case TRADE_RETCODE_REQUOTE             : return 138; /* ERR_REQUOTE */
			case TRADE_RETCODE_LOCKED              : return 139; /* ERR_ORDER_LOCKED */
			//case TRADE_RETCODE_LONG_ONLY         : return 140; /* ERR_LONG_POSITIONS_ONLY_ALLOWED */
			case TRADE_RETCODE_TOO_MANY_REQUESTS   : return 141; /* ERR_TOO_MANY_REQUESTS */
			//case ERR_TRADE_MODIFY_DENIED         : return 145; /* ERR_TRADE_MODIFY_DENIED */
			//case ERR_TRADE_CONTEXT_BUSY          : return 146; /* ERR_TRADE_CONTEXT_BUSY */
			case TRADE_RETCODE_INVALID_EXPIRATION  : return 147; /* ERR_TRADE_EXPIRATION_DENIED */
			case TRADE_RETCODE_LIMIT_ORDERS        : return 148; /* ERR_TRADE_TOO_MANY_ORDERS */
			// TRADE_RETCODE_HEDGE_PROHIBITED is listed in MQL5's documentation as a value, but it's not defined as a constant
			case 10046                             : return 149; /* ERR_TRADE_HEDGE_PROHIBITED */
			case TRADE_RETCODE_FIFO_CLOSE          : return 150; /* ERR_TRADE_PROHIBITED_BY_FIFO */
	
			//--- mql4 run time errors
			//case ERR_NO_MQLERROR                 : return 4000; /* ERR_NO_MQLERROR */
			case ERR_INVALID_POINTER_TYPE          : return 4001; /* ERR_WRONG_FUNCTION_POINTER */
			case ERR_SMALL_ARRAY                   : return 4002; /* ERR_ARRAY_INDEX_OUT_OF_RANGE */
			//case ERR_NOT_ENOUGH_MEMORY           : return 4003; /* ERR_NO_MEMORY_FOR_CALL_STACK */
			case ERR_MATH_OVERFLOW                 : return 4004; /* ERR_RECURSIVE_STACK_OVERFLOW */
			//case ERR_NOT_ENOUGH_STACK_FOR_PARAM  : return 4005; /* ERR_NOT_ENOUGH_STACK_FOR_PARAM */
			case ERR_STRING_OUT_OF_MEMORY          : return 4006; /* ERR_NO_MEMORY_FOR_PARAM_STRING */
			//case ERR_NO_MEMORY_FOR_TEMP_STRING   : return 4007; /* ERR_NO_MEMORY_FOR_TEMP_STRING */
			case ERR_NOTINITIALIZED_STRING         : return 4008; /* ERR_NOT_INITIALIZED_STRING */
			//case ERR_NOT_INITIALIZED_ARRAYSTRING : return 4009; /* ERR_NOT_INITIALIZED_ARRAYSTRING */
			//case ERR_NO_MEMORY_FOR_ARRAYSTRING   : return 4010; /* ERR_NO_MEMORY_FOR_ARRAYSTRING */
			case ERR_STRING_TOO_BIGNUMBER          : return 4011; /* ERR_TOO_LONG_STRING */
			//case ERR_REMAINDER_FROM_ZERO_DIVIDE  : return 4012; /* ERR_REMAINDER_FROM_ZERO_DIVIDE */
			//case ERR_ZERO_DIVIDE                 : return 4013; /* ERR_ZERO_DIVIDE */
			//case ERR_UNKNOWN_COMMAND             : return 4014; /* ERR_UNKNOWN_COMMAND */
			//case ERR_WRONG_JUMP                  : return 4015; /* ERR_WRONG_JUMP */
			case ERR_ZEROSIZE_ARRAY                : return 4016; /* ERR_NOT_INITIALIZED_ARRAY */
			//case ERR_DLL_CALLS_NOT_ALLOWED       : return 4017; /* ERR_DLL_CALLS_NOT_ALLOWED */
			//case ERR_CANNOT_LOAD_LIBRARY         : return 4018; /* ERR_CANNOT_LOAD_LIBRARY */
			//case ERR_CANNOT_CALL_FUNCTION        : return 4019; /* ERR_CANNOT_CALL_FUNCTION */
			//case ERR_EXTERNAL_CALLS_NOT_ALLOWED  : return 4020; /* ERR_EXTERNAL_CALLS_NOT_ALLOWED */
			//case ERR_NO_MEMORY_FOR_RETURNED_STR  : return 4021; /* ERR_NO_MEMORY_FOR_RETURNED_STR */
			//case ERR_SYSTEM_BUSY                 : return 4022; /* ERR_SYSTEM_BUSY */
			//case ERR_DLLFUNC_CRITICALERROR       : return 4023; /* ERR_DLLFUNC_CRITICALERROR */
			case ERR_INTERNAL_ERROR                : return 4024; /* ERR_INTERNAL_ERROR */
			case ERR_NOT_ENOUGH_MEMORY             : return 4025; /* ERR_OUT_OF_MEMORY */
			case ERR_INVALID_POINTER               : return 4026; /* ERR_INVALID_POINTER */
			case ERR_TOO_MANY_FORMATTERS           : return 4027; /* ERR_FORMAT_TOO_MANY_FORMATTERS */
			case ERR_TOO_MANY_PARAMETERS           : return 4028; /* ERR_FORMAT_TOO_MANY_PARAMETERS */
			case ERR_INVALID_ARRAY                 : return 4029; /* ERR_ARRAY_INVALID */
			case ERR_CHART_NO_REPLY                : return 4030; /* ERR_CHART_NOREPLY */
			//case ERR_INVALID_FUNCTION_PARAMSCNT  : return 4050; /* ERR_INVALID_FUNCTION_PARAMSCNT */
			//case ERR_INVALID_FUNCTION_PARAMVALUE : return 4051; /* ERR_INVALID_FUNCTION_PARAMVALUE */
			case ERR_WRONG_INTERNAL_PARAMETER      : return 4052; /* ERR_STRING_FUNCTION_INTERNAL */
			//case ERR_SOME_ARRAY_ERROR            : return 4053; /* ERR_SOME_ARRAY_ERROR */
			case ERR_SERIES_ARRAY                  : return 4054; /* ERR_INCORRECT_SERIESARRAY_USING */
			//case ERR_CUSTOM_INDICATOR_ERROR      : return 4055; /* ERR_CUSTOM_INDICATOR_ERROR */
			case ERR_INCOMPATIBLE_ARRAYS           : return 4056; /* ERR_INCOMPATIBLE_ARRAYS */
			case ERR_GLOBALVARIABLE_EXISTS         :
			case ERR_GLOBALVARIABLE_NOT_MODIFIED   :
			case ERR_GLOBALVARIABLE_CANNOTREAD     :
			case ERR_GLOBALVARIABLE_CANNOTWRITE    : return 4057; /* ERR_GLOBAL_VARIABLES_PROCESSING */
			case ERR_GLOBALVARIABLE_NOT_FOUND      : return 4058; /* ERR_GLOBAL_VARIABLE_NOT_FOUND */
			//case ERR_FUNC_NOT_ALLOWED_IN_TESTING : return 4059; /* ERR_FUNC_NOT_ALLOWED_IN_TESTING */
			case ERR_FUNCTION_NOT_ALLOWED          : return 4060; /* ERR_FUNCTION_NOT_CONFIRMED */
			case ERR_MAIL_SEND_FAILED              : return 4061; /* ERR_SEND_MAIL_ERROR */
			//case ERR_STRING_PARAMETER_EXPECTED   : return 4062; /* ERR_STRING_PARAMETER_EXPECTED */
			//case ERR_INTEGER_PARAMETER_EXPECTED  : return 4063; /* ERR_INTEGER_PARAMETER_EXPECTED */
			//case ERR_DOUBLE_PARAMETER_EXPECTED   : return 4064; /* ERR_DOUBLE_PARAMETER_EXPECTED */
			//case ERR_ARRAY_AS_PARAMETER_EXPECTED : return 4065; /* ERR_ARRAY_AS_PARAMETER_EXPECTED */
			//case ERR_HISTORY_WILL_UPDATED        : return 4066; /* ERR_HISTORY_WILL_UPDATED */
			//case ERR_TRADE_ERROR                 : return 4067; /* ERR_TRADE_ERROR */
			case ERR_RESOURCE_NOT_FOUND            : return 4068; /* ERR_RESOURCE_NOT_FOUND */
			case ERR_RESOURCE_UNSUPPOTED_TYPE      : return 4069; /* ERR_RESOURCE_NOT_SUPPORTED */
			case ERR_RESOURCE_NAME_DUPLICATED      : return 4070; /* ERR_RESOURCE_DUPLICATED */
			case ERR_INDICATOR_CANNOT_CREATE       : return 4071; /* ERR_INDICATOR_CANNOT_INIT */
			case ERR_INDICATOR_CANNOT_ADD          :
			case ERR_CHART_INDICATOR_CANNOT_ADD    : return 4072; /* ERR_INDICATOR_CANNOT_LOAD */
			case ERR_HISTORY_NOT_FOUND             : return 4073; /* ERR_NO_HISTORY_DATA */
			case ERR_HISTORY_LOAD_ERRORS           : return 4074; /* ERR_NO_MEMORY_FOR_HISTORY */
			case ERR_BUFFERS_NO_MEMORY             : return 4075; /* ERR_NO_MEMORY_FOR_INDICATOR */
			case ERR_FILE_ENDOFFILE                : return 4099; /* ERR_END_OF_FILE */
			// The file errors below have duplicate errors below around code 5010
			//case ERR_SOME_FILE_ERROR             : return 4100; /* ERR_SOME_FILE_ERROR */
			//case ERR_WRONG_FILENAME              : return 4101; /* ERR_WRONG_FILE_NAME */
			//case ERR_TOO_MANY_FILES              : return 4102; /* ERR_TOO_MANY_OPENED_FILES */
			//case ERR_CANNOT_OPEN_FILE            : return 4103; /* ERR_CANNOT_OPEN_FILE */
			//case ERR_INCOMPATIBLE_FILE           : return 4104; /* ERR_INCOMPATIBLE_FILEACCESS */
			case ERR_TRADE_POSITION_NOT_FOUND      :
			case ERR_TRADE_ORDER_NOT_FOUND         :
			case ERR_TRADE_DEAL_NOT_FOUND          : return 4105; /* ERR_NO_ORDER_SELECTED */
			case ERR_MARKET_UNKNOWN_SYMBOL         :
			case ERR_INDICATOR_UNKNOWN_SYMBOL      : return 4106; /* ERR_UNKNOWN_SYMBOL */
			//case ERR_INVALID_PRICE_PARAM         : return 4107; /* ERR_INVALID_PRICE_PARAM */
			//case ERR_INVALID_TICKET              : return 4108; /* ERR_INVALID_TICKET */
			case ERR_TRADE_DISABLED                :
			case TRADE_RETCODE_CLIENT_DISABLES_AT  : return 4109; /* ERR_TRADE_NOT_ALLOWED */
			case TRADE_RETCODE_SHORT_ONLY          : return 4110; /* ERR_LONGS_NOT_ALLOWED */
			case TRADE_RETCODE_LONG_ONLY           : return 4111; /* ERR_SHORTS_NOT_ALLOWED */
			case TRADE_RETCODE_SERVER_DISABLES_AT  : return 4112; /* ERR_TRADE_EXPERT_DISABLED_BY_SERVER */
			//case ERR_OBJECT_ALREADY_EXISTS       : return 4200; /* ERR_OBJECT_ALREADY_EXISTS */ // MQL5 doesn't give error when an object with the same name is created
			case ERR_OBJECT_WRONG_PROPERTY         : return 4201; /* ERR_UNKNOWN_OBJECT_PROPERTY */
			case ERR_OBJECT_NOT_FOUND              : return 4202; /* ERR_OBJECT_DOES_NOT_EXIST */
			//case ERR_INVALID_PARAMETER           : return 4203; /* ERR_UNKNOWN_OBJECT_TYPE */ // Value found after testing
			//case ERR_WRONG_STRING_PARAMETER      : return 4204; /* ERR_NO_OBJECT_NAME */ // Value found after testing
			//case ERR_OBJECT_COORDINATES_ERROR    : return 4205; /* ERR_OBJECT_COORDINATES_ERROR */
			//case ERR_INVALID_PARAMETER           : return 4206; /* ERR_NO_SPECIFIED_SUBWINDOW */ // Value found after testing
			case ERR_OBJECT_ERROR                  : return 4207; /* ERR_SOME_OBJECT_ERROR */
			case ERR_CHART_WRONG_PROPERTY          : return 4210; /* ERR_CHART_PROP_INVALID */
			case ERR_CHART_NOT_FOUND               : return 4211; /* ERR_CHART_NOT_FOUND */
			case ERR_CHART_WINDOW_NOT_FOUND        : return 4212; /* ERR_CHARTWINDOW_NOT_FOUND */
			case ERR_CHART_INDICATOR_NOT_FOUND     : return 4213; /* ERR_CHARTINDICATOR_NOT_FOUND */
			case ERR_MARKET_NOT_SELECTED           : return 4220; /* ERR_SYMBOL_SELECT */
			case ERR_NOTIFICATION_SEND_FAILED      : return 4250; /* ERR_NOTIFICATION_ERROR */
			case ERR_NOTIFICATION_WRONG_PARAMETER  : return 4251; /* ERR_NOTIFICATION_PARAMETER */
			case ERR_NOTIFICATION_WRONG_SETTINGS   : return 4252; /* ERR_NOTIFICATION_SETTINGS */
			case ERR_NOTIFICATION_TOO_FREQUENT     : return 4253; /* ERR_NOTIFICATION_TOO_FREQUENT */
			case ERR_FTP_NOSERVER                  : return 4260; /* ERR_FTP_NOSERVER */
			case ERR_FTP_NOLOGIN                   : return 4261; /* ERR_FTP_NOLOGIN */
			case ERR_FTP_CONNECT_FAILED            : return 4262; /* ERR_FTP_CONNECT_FAILED  */
			// ERR_FTP_CLOSED is listed in MQL5's documentation as a value, but it's not defined as a constant
			case 4524                              : return 4263; /* ERR_FTP_CLOSED */
			case ERR_FTP_CHANGEDIR                 : return 4264; /* ERR_FTP_CHANGEDIR */
			case ERR_FTP_FILE_ERROR                : return 4265; /* ERR_FTP_FILE_ERROR */
			case ERR_FTP_SEND_FAILED               : return 4266; /* ERR_FTP_ERROR */
			case ERR_TOO_MANY_FILES                : return 5001; /* ERR_FILE_TOO_MANY_OPENED */
			case ERR_WRONG_FILENAME                : return 5002; /* ERR_FILE_WRONG_FILENAME */
			case ERR_TOO_LONG_FILENAME             : return 5003; /* ERR_FILE_TOO_LONG_FILENAME */
			case ERR_CANNOT_OPEN_FILE              : return 5004; /* ERR_FILE_CANNOT_OPEN */
			case ERR_FILE_CACHEBUFFER_ERROR        : return 5005; /* ERR_FILE_BUFFER_ALLOCATION_ERROR */
			case ERR_CANNOT_DELETE_FILE            : return 5006; /* ERR_FILE_CANNOT_DELETE */
			case ERR_INVALID_FILEHANDLE            : return 5007; /* ERR_FILE_INVALID_HANDLE */
			case ERR_WRONG_FILEHANDLE              : return 5008; /* ERR_FILE_WRONG_HANDLE */
			case ERR_FILE_NOTTOWRITE               : return 5009; /* ERR_FILE_NOT_TOWRITE */
			case ERR_FILE_NOTTOREAD                : return 5010; /* ERR_FILE_NOT_TOREAD */
			case ERR_FILE_NOTBIN                   : return 5011; /* ERR_FILE_NOT_BIN */
			case ERR_FILE_NOTTXT                   : return 5012; /* ERR_FILE_NOT_TXT */
			case ERR_FILE_NOTTXTORCSV              : return 5013; /* ERR_FILE_NOT_TXTORCSV */
			case ERR_FILE_NOTCSV                   : return 5014; /* ERR_FILE_NOT_CSV */
			case ERR_FILE_READERROR                : return 5015; /* ERR_FILE_READ_ERROR */
			case ERR_FILE_WRITEERROR               : return 5016; /* ERR_FILE_WRITE_ERROR */
			case ERR_FILE_BINSTRINGSIZE            : return 5017; /* ERR_FILE_BIN_STRINGSIZE */
			case ERR_INCOMPATIBLE_FILE             : return 5018; /* ERR_FILE_INCOMPATIBLE */
			case ERR_FILE_IS_DIRECTORY             : return 5019; /* ERR_FILE_IS_DIRECTORY */
			case ERR_FILE_NOT_EXIST                : return 5020; /* ERR_FILE_NOT_EXIST */
			case ERR_FILE_CANNOT_REWRITE           : return 5021; /* ERR_FILE_CANNOT_REWRITE */
			case ERR_WRONG_DIRECTORYNAME           : return 5022; /* ERR_FILE_WRONG_DIRECTORYNAME */
			case ERR_DIRECTORY_NOT_EXIST           : return 5023; /* ERR_FILE_DIRECTORY_NOT_EXIST */
			case ERR_FILE_ISNOT_DIRECTORY          : return 5024; /* ERR_FILE_NOT_DIRECTORY */
			case ERR_CANNOT_DELETE_DIRECTORY       : return 5025; /* ERR_FILE_CANNOT_DELETE_DIRECTORY */
			case ERR_CANNOT_CLEAN_DIRECTORY        : return 5026; /* ERR_FILE_CANNOT_CLEAN_DIRECTORY */
			case ERR_ARRAY_RESIZE_ERROR            : return 5027; /* ERR_FILE_ARRAYRESIZE_ERROR */
			case ERR_STRING_RESIZE_ERROR           : return 5028; /* ERR_FILE_STRINGRESIZE_ERROR */
			case ERR_STRUCT_WITHOBJECTS_ORCLASS    : return 5029; /* ERR_FILE_STRUCT_WITH_OBJECTS */
			case ERR_WEBREQUEST_INVALID_ADDRESS    : return 5200; /* ERR_WEBREQUEST_INVALID_ADDRESS */
			case ERR_WEBREQUEST_CONNECT_FAILED     : return 5201; /* ERR_WEBREQUEST_CONNECT_FAILED */
			case ERR_WEBREQUEST_TIMEOUT            : return 5202; /* ERR_WEBREQUEST_TIMEOUT */
			case ERR_WEBREQUEST_REQUEST_FAILED     : return 5203; /* ERR_WEBREQUEST_REQUEST_FAILED */
			case ERR_USER_ERROR_FIRST              : return 65536; /* ERR_USER_ERROR_FIRST */
	
			// There is no something like ERR_COMMON_ERROR in MQL5, but for example ERR_INVALID_PARAMETER is returned
			// for what should be ERR_UNKNOWN_OBJECT_TYPE or ERR_NO_SPECIFIED_SUBWINDOW. Instead of deciding which one
			// to return, return ERR_COMMON_ERROR
			default : return 2; /* ERR_COMMON_ERROR */
		}
	}
	
	static void HideTestIndicators(bool hide) {
	   // https://www.mql5.com/en/forum/72182
		if (::MQLInfoInteger(MQL_VISUAL_MODE)) {
			::Print("Sorry, HideTestIndicators() does not work for MQL5");
		}
	}
	
	static int Hour() {
		MqlDateTime tm;
		::TimeCurrent(tm);
	
		return tm.hour;
	}
	
	static bool IsOptimization() {
		return (bool)::MQLInfoInteger(MQL_OPTIMIZATION);
	}
	
	static bool IsTesting() {
		return (bool)::MQLInfoInteger(MQL_TESTER);
	}
	
	static bool IsTradeAllowed() {
		if (
			   !::TerminalInfoInteger(TERMINAL_TRADE_ALLOWED) // The "Algo Trading" button is off
			|| !::MQLInfoInteger(MQL_TRADE_ALLOWED)           // The "Allow Algo Trading" checkbox (when the program is added) is not checked
			|| !::AccountInfoInteger(ACCOUNT_TRADE_ALLOWED)   // Trading is forbidden for the account
			|| !::AccountInfoInteger(ACCOUNT_TRADE_EXPERT)    // Automated trading is forbidden for the account
		) return false;
	
		return true;
	}
	
	static bool IsVisualMode() {
		return (bool)::MQLInfoInteger(MQL_VISUAL_MODE);
	}
	
	static double MarketInfo(string symbol, int type) {
		// For most cases below this is not needed, but OrderCalcMargin() returns error 5040 (Damaged parameter of string type) if the symbol is NULL
		if (symbol == NULL) symbol = ::Symbol();
	
		switch(type) {
			case 1 /* MODE_LOW                */ : return ::SymbolInfoDouble(symbol, SYMBOL_LASTLOW);
			case 2 /* MODE_HIGH               */ : return ::SymbolInfoDouble(symbol, SYMBOL_LASTHIGH);
			case 5 /* MODE_TIME               */ : return (double)::SymbolInfoInteger(symbol, SYMBOL_TIME);
			case 9 /* MODE_BID                */ : return ::SymbolInfoDouble(symbol, SYMBOL_BID);
			case 10 /* MODE_ASK               */ : return ::SymbolInfoDouble(symbol, SYMBOL_ASK);
			case 11 /* MODE_POINT             */ : return ::SymbolInfoDouble(symbol, SYMBOL_POINT);
			case 12 /* MODE_DIGITS            */ : return (double)::SymbolInfoInteger(symbol, SYMBOL_DIGITS);
			case 13 /* MODE_SPREAD            */ : return (double)::SymbolInfoInteger(symbol, SYMBOL_SPREAD);
			case 14 /* MODE_STOPLEVEL         */ : return (double)::SymbolInfoInteger(symbol, SYMBOL_TRADE_STOPS_LEVEL);
			case 15 /* MODE_LOTSIZE           */ : return ::SymbolInfoDouble(symbol, SYMBOL_TRADE_CONTRACT_SIZE);
			case 16 /* MODE_TICKVALUE         */ : return ::SymbolInfoDouble(symbol, SYMBOL_TRADE_TICK_VALUE);
			case 17 /* MODE_TICKSIZE          */ : return ::SymbolInfoDouble(symbol, SYMBOL_TRADE_TICK_SIZE);
			case 18 /* MODE_SWAPLONG          */ : return ::SymbolInfoDouble(symbol, SYMBOL_SWAP_LONG);
			case 19 /* MODE_SWAPSHORT         */ : return ::SymbolInfoDouble(symbol, SYMBOL_SWAP_SHORT);
			case 20 /* MODE_STARTING          */ : return (double)::SymbolInfoInteger(symbol, SYMBOL_START_TIME);
			case 21 /* MODE_EXPIRATION        */ : return (double)::SymbolInfoInteger(symbol, SYMBOL_EXPIRATION_TIME);
			case 22 /* MODE_TRADEALLOWED      */ : return (::SymbolInfoInteger(symbol, SYMBOL_TRADE_MODE) != SYMBOL_TRADE_MODE_DISABLED);
			case 23 /* MODE_MINLOT            */ : return ::SymbolInfoDouble(symbol, SYMBOL_VOLUME_MIN);
			case 24 /* MODE_LOTSTEP           */ : return ::SymbolInfoDouble(symbol, SYMBOL_VOLUME_STEP);
			case 25 /* MODE_MAXLOT            */ : return ::SymbolInfoDouble(symbol, SYMBOL_VOLUME_MAX);
			case 26 /* MODE_SWAPTYPE          */ : return (double)::SymbolInfoInteger(symbol, SYMBOL_SWAP_MODE);
			case 27 /* MODE_PROFITCALCMODE    */ : return (double)::SymbolInfoInteger(symbol, SYMBOL_TRADE_CALC_MODE);
			case 28 /* MODE_MARGINCALCMODE    */ : return (double)::SymbolInfoInteger(symbol, SYMBOL_TRADE_CALC_MODE);
			case 29 /* MODE_MARGININIT        */ : return (double)::SymbolInfoDouble(symbol, SYMBOL_MARGIN_INITIAL);
			case 30 /* MODE_MARGINMAINTENANCE */ : return (double)::SymbolInfoDouble(symbol, SYMBOL_MARGIN_MAINTENANCE);
			case 31 /* MODE_MARGINHEDGED      */ : return (double)::SymbolInfoDouble(symbol, SYMBOL_MARGIN_HEDGED);
			case 32 /* MODE_MARGINREQUIRED    */ :	{
				// Free margin required to open 1 lot for buying
			   double margin = 0.0;
	
				if (::OrderCalcMargin(ORDER_TYPE_BUY, symbol, 1, ::SymbolInfoDouble(symbol, SYMBOL_ASK), margin))
					return margin;
				else
					return 0.0;
			}
			case 33 /* MODE_FREEZELEVEL */     : return (double)::SymbolInfoInteger(symbol, SYMBOL_TRADE_FREEZE_LEVEL);
			case 34 /* MODE_CLOSEBY_ALLOWED */ : return 0.0;
		}
	
		return 0.0;
	}
	
	static int Minute() {
		MqlDateTime tm;
		::TimeCurrent(tm);
	
		return tm.min;
	}
	
	static bool ObjectCreate(
		long chart_id, string object_name, ENUM_OBJECT object_type, int sub_window,
		datetime time1, double price1,
		datetime time2 = 0, double price2 = 0,
		datetime time3 = 0, double price3 = 0,
		datetime time4 = 0, double price4 = 0,
		datetime time5 = 0, double price5 = 0,
		datetime time6 = 0, double price6 = 0,
		datetime time7 = 0, double price7 = 0,
		datetime time8 = 0, double price8 = 0,
		datetime time9 = 0, double price9 = 0,
		datetime time10 = 0, double price10 = 0,
		datetime time11 = 0, double price11 = 0,
		datetime time12 = 0, double price12 = 0,
		datetime time13 = 0, double price13 = 0,
		datetime time14 = 0, double price14 = 0,
		datetime time15 = 0, double price15 = 0,
		datetime time16 = 0, double price16 = 0,
		datetime time17 = 0, double price17 = 0,
		datetime time18 = 0, double price18 = 0,
		datetime time19 = 0, double price19 = 0,
		datetime time20 = 0, double price20 = 0,
		datetime time21 = 0, double price21 = 0,
		datetime time22 = 0, double price22 = 0,
		datetime time23 = 0, double price23 = 0,
		datetime time24 = 0, double price24 = 0,
		datetime time25 = 0, double price25 = 0,
		datetime time26 = 0, double price26 = 0,
		datetime time27 = 0, double price27 = 0,
		datetime time28 = 0, double price28 = 0,
		datetime time29 = 0, double price29 = 0
	) {
		return (bool)::ObjectCreate(
			chart_id, object_name, object_type, sub_window,
			time1, price1,
			time2, price2,
			time3, price3,
			time4, price4,
			time5, price5,
			time6, price6,
			time7, price7,
			time8, price8,
			time9, price9,
			time10, price10,
			time11, price11,
			time12, price12,
			time13, price13,
			time14, price14,
			time15, price15,
			time16, price16,
			time17, price17,
			time18, price18,
			time19, price19,
			time20, price20,
			time21, price21,
			time22, price22,
			time23, price23,
			time24, price24,
			time25, price25,
			time26, price26,
			time27, price27,
			time28, price28,
			time29, price29
			);
	}
	
	static bool ObjectCreate(
		string object_name, ENUM_OBJECT object_type, int sub_window,
		datetime time1, double price1,
		datetime time2 = 0, double price2 = 0,
		datetime time3 = 0, double price3 = 0
	) {
		return (bool)::ObjectCreate(0, object_name, object_type, sub_window, time1, price1, time2, price2, time3, price3);
	}
	
	static int ObjectFind(long chart_id, string object_name) {
		return ::ObjectFind(chart_id, object_name);
	}
	static int ObjectFind(string object_name) {
		return ::ObjectFind(0, object_name);
	}
	
	/**
	* In MQL5 the names of the constants in ENUM_OBJECT_PROPERTY_* are pretty much the same as in MQL4, so when constants are used the functions below will serve
	*/
	static long ObjectGetInteger(long chart_id, const string object_name, ENUM_OBJECT_PROPERTY_INTEGER prop_id, int prop_modifier = 0) {
		return ::ObjectGetInteger(chart_id, object_name, prop_id, prop_modifier);
	}
	static bool ObjectGetInteger(long chart_id, const string object_name, ENUM_OBJECT_PROPERTY_INTEGER prop_id, int prop_modifier, long & long_var) {
		return ::ObjectGetInteger(chart_id, object_name, prop_id, prop_modifier, long_var);
	}
	/**
	* These overloads are used just in case when integer value is passed to prop_id.
	* It's presumed that this integer value is what represents the enumeration constants in MQL4, which representation is different in MQL5.
	*/
	static long ObjectGetInteger(long chart_id, const string object_name, int prop_id, int prop_modifier = 0) {
		ENUM_OBJECT_PROPERTY_INTEGER propID;
	
		switch (prop_id) {
			case 0 /* OBJPROP_PRICE1 */ : propID = OBJPROP_TIME; prop_modifier = 0; break;
			case 2 /* OBJPROP_PRICE2 */ : propID = OBJPROP_TIME; prop_modifier = 1; break;
			case 4 /* OBJPROP_PRICE3 */ : propID = OBJPROP_TIME; prop_modifier = 2; break;
			default : {
				propID = CFAE::_ConvertEnumObjectPropertyInteger_(prop_id);
			}
		}
	
		if (propID == -1) return 0;
	
		return ::ObjectGetInteger(chart_id, object_name, propID, prop_modifier);
	}
	static bool ObjectGetInteger(long chart_id, const string object_name, int prop_id, int prop_modifier, long & long_var) {
		ENUM_OBJECT_PROPERTY_INTEGER propID;
	
		switch (prop_id) {
			case 0 /* OBJPROP_PRICE1 */ : propID = OBJPROP_TIME; prop_modifier = 0; break;
			case 2 /* OBJPROP_PRICE2 */ : propID = OBJPROP_TIME; prop_modifier = 1; break;
			case 4 /* OBJPROP_PRICE3 */ : propID = OBJPROP_TIME; prop_modifier = 2; break;
			default : {
				propID = CFAE::_ConvertEnumObjectPropertyInteger_(prop_id);
			}
		}
	
		if (propID == -1) {
			long_var = 0;
			return true;
		}
	
		return ::ObjectGetInteger(chart_id, object_name, propID, prop_modifier, long_var);
	}
	
	/**
	* Overloads to cover cases when the property is an enumeration.
	* This works for all MQL5 enum constants, such as OBJPROP_COLOR...
	*/
	static int ObjectSet(string name, ENUM_OBJECT_PROPERTY_INTEGER prop_id, long value) {
		return (int)::ObjectSetInteger(0, name, prop_id, 0, value);
	}
	static double ObjectSet(string name, ENUM_OBJECT_PROPERTY_DOUBLE prop_id, double value) {
		return (int)::ObjectSetDouble(0, name, prop_id, 0, value);
	}
	/**
	* Overload to cover cases when the property is an integer value.
	* Also works when the property is a constant defined with #define
	*/
	static double ObjectSet(string name, int index, double value) {
		ENUM_OBJECT_PROPERTY_INTEGER propInteger = -1;
		ENUM_OBJECT_PROPERTY_DOUBLE propDouble   = -1;
		int propModifier = 0;
		double output    = 0.0;
	
		// 2) Integer type
		switch (index) {
			// For the first ones the constants should be defined with #define
			case 0 /* OBJPROP_TIME1 */        : propInteger = OBJPROP_TIME; propModifier = 0; break;
			case 2 /* OBJPROP_TIME2 */        : propInteger = OBJPROP_TIME; propModifier = 1; break;
			case 4 /* OBJPROP_TIME3 */        : propInteger = OBJPROP_TIME; propModifier = 2; break;
			case 200 /* OBJPROP_FIBOLEVELS */ : propInteger = OBJPROP_LEVELS; break;
			
			case 6   : propInteger = OBJPROP_COLOR; break;
			case 7   : propInteger = OBJPROP_STYLE; break;
			case 8   : propInteger = OBJPROP_WIDTH; break;
			case 9   : propInteger = OBJPROP_BACK; break;
			case 10  : propInteger = OBJPROP_RAY; break;
			case 11  : propInteger = OBJPROP_ELLIPSE; break;
			case 14  : propInteger = OBJPROP_ARROWCODE; break;
			case 15  : propInteger = OBJPROP_TIMEFRAMES; break;
			case 100 : propInteger = OBJPROP_FONTSIZE; break;
			case 101 : propInteger = OBJPROP_CORNER; break;
			case 102 : propInteger = OBJPROP_XDISTANCE; break;
			case 103 : propInteger = OBJPROP_YDISTANCE; break;
			case 201 : propInteger = OBJPROP_LEVELCOLOR; break;
			case 202 : propInteger = OBJPROP_LEVELSTYLE; break;
			case 203 : propInteger = OBJPROP_LEVELWIDTH; break;
		}
	
		if (propInteger > -1) output = (double)::ObjectSetInteger(0, name, propInteger, propModifier, (int)value);
	
		// 2) Double type
		switch (index) {
			// For the first ones the constants should be defined with #define
			case 1 /* OBJPROP_PRICE1 */ : propDouble = OBJPROP_PRICE; propModifier = 0; break;
			case 3 /* OBJPROP_PRICE2 */ : propDouble = OBJPROP_PRICE; propModifier = 1; break;
			case 5 /* OBJPROP_PRICE3 */ : propDouble = OBJPROP_PRICE; propModifier = 2; break;
	
			case 12 : propDouble = OBJPROP_SCALE; break;
			case 13 : propDouble = OBJPROP_ANGLE; break;
			case 16 : propDouble = OBJPROP_DEVIATION; break;
		}
	
		if (propDouble > -1) output = ::ObjectSetDouble(0, name, propDouble, propModifier, value);
	
		// 3) OBJPROP_FIRSTLEVEL+n
		if (index >= 210 && index <= 241) {
			propModifier = index - 210;
			output = ::ObjectSetDouble(0, name, OBJPROP_LEVELVALUE, propModifier, value);
		}
		
		return output;
	}
	
	/**
	* These overloads are used just in case when integer value is passed to prop_id.
	* It's presumed that this integer value is what represents the enumeration constants in MQL4, which representation is different in MQL5.
	*/
	static bool ObjectSetInteger(long chart_id, const string object_name, ENUM_OBJECT_PROPERTY_INTEGER prop_id, long prop_value) {
		return ::ObjectSetInteger(chart_id, object_name, prop_id, prop_value);
	}
	static bool ObjectSetInteger(long chart_id, const string object_name, ENUM_OBJECT_PROPERTY_INTEGER prop_id, int prop_modifier, long prop_value) {
		return ::ObjectSetInteger(chart_id, object_name, prop_id, prop_modifier, prop_value);
	}
	static bool ObjectSetInteger(long chart_id, const string object_name, int prop_id, long prop_value) {
		ENUM_OBJECT_PROPERTY_INTEGER propID = CFAE::_ConvertEnumObjectPropertyInteger_(prop_id);
		if (propID == -1) return false;
	
		return ::ObjectSetInteger(chart_id, object_name, propID, prop_value);
	}
	static bool ObjectSetInteger(long chart_id, const string object_name, int prop_id, int prop_modifier, long prop_value) {
		ENUM_OBJECT_PROPERTY_INTEGER propID = CFAE::_ConvertEnumObjectPropertyInteger_(prop_id);
		if (propID == -1) return false;
	
		return ::ObjectSetInteger(chart_id, object_name, propID, prop_modifier, prop_value);
	}
	
	/**
	* These overloads are used just in case when integer value is passed to prop_id.
	* It's presumed that this integer value is what represents the enumeration constants in MQL4, which representation is different in MQL5.
	*/
	static bool ObjectSetString(long chart_id, const string object_name, ENUM_OBJECT_PROPERTY_STRING prop_id, string prop_value) {
		return ::ObjectSetString(chart_id, object_name, prop_id, prop_value);
	}
	static bool ObjectSetString(long chart_id, const string object_name, ENUM_OBJECT_PROPERTY_STRING prop_id, int prop_modifier, string prop_value) {
		return ::ObjectSetString(chart_id, object_name, prop_id, prop_modifier, prop_value);
	}
	static bool ObjectSetString(long chart_id, const string object_name, int prop_id, string prop_value) {
		ENUM_OBJECT_PROPERTY_STRING propID = CFAE::_ConvertEnumObjectPropertyString_(prop_id);
		if (propID == -1) return true;
	
		return ::ObjectSetString(chart_id, object_name, propID, prop_value);
	}
	static bool ObjectSetString(long chart_id, const string object_name, int prop_id, int prop_modifier, string prop_value) {
		ENUM_OBJECT_PROPERTY_STRING propID = CFAE::_ConvertEnumObjectPropertyString_(prop_id);
		if (propID == -1) return true;
	
		return ::ObjectSetString(chart_id, object_name, propID, prop_modifier, prop_value);
	}
	
	static bool ObjectSetText(string object_name, string text, int font_size = 0, string font_name = NULL, color text_color = clrNONE) {
		bool output = ::ObjectSetString(0, object_name, OBJPROP_TEXT, text);
	
		ENUM_OBJECT objType = (ENUM_OBJECT)::ObjectGetInteger(0, object_name, OBJPROP_TYPE);
	
		// According to the documentation, the later 3 parameters are used only for OBJ_TEXT and OBJ_LABEL
		if (objType == OBJ_TEXT || objType == OBJ_LABEL) {
			if (font_size > 0) ::ObjectSetInteger(0, object_name, OBJPROP_FONTSIZE, font_size);
	
			if (font_name != NULL) ::ObjectSetString(0, object_name, OBJPROP_FONT, font_name);
	
			if (text_color != clrNONE) ::ObjectSetInteger(0, object_name, OBJPROP_COLOR, text_color);
		}
	
		return output;
	}
	
	static int ObjectsDeleteAll(int sub_window = -1, int object_type = -1) {
		return ::ObjectsDeleteAll(0, sub_window, object_type);
	}
	
	static bool OrderClose(long ticket, double lots, double price, int slippage, color arrow_color = clrNONE) {
		// ticket is actually position id, so find the position by its id
		int positionsTotal = ::PositionsTotal();
		bool found = false;
		long positionID = ticket;
	
		// try to find the position by position ID
		for (int index = positionsTotal-1; index >= 0; index--) {
			ticket = (long)::PositionGetTicket(index);
			if (::PositionGetInteger(POSITION_IDENTIFIER) == positionID) {
				found = true;
				break;
			}
		}
	
		/*
		// try to find the position by deal ticket
		if (!found) {
			if (::HistoryDealSelect(ticket))	{
				long posID = ::HistoryDealGetInteger(ticket, DEAL_POSITION_ID);
	
				for (int index = positionsTotal-1; index >= 0; index--) {
					ticket = (long)::PositionGetTicket(index);
					
					if (::PositionGetInteger(POSITION_IDENTIFIER) == posID) {
						found = true;
						break;
					}
				}
			}
		}
		*/
	
		if (!found) return false;
	
		double lots0   = ::NormalizeDouble(PositionGetDouble(POSITION_VOLUME), 5);
		string symbol  = ::PositionGetString(POSITION_SYMBOL);
		double lotstep = ::SymbolInfoDouble(symbol, SYMBOL_VOLUME_STEP);
	
		while (true) {
			//-- fixing -------------------------------------------------------
			lots = ::MathFloor(lots/lotstep)*lotstep;
	
			//-- close --------------------------------------------------------
			MqlTradeRequest request;
			MqlTradeResult result;
			::ZeroMemory(request);
			::ZeroMemory(result);
	
			request.action    = TRADE_ACTION_DEAL;
			request.price     = price;
			request.type      = (::PositionGetInteger(POSITION_TYPE) == POSITION_TYPE_BUY) ? ORDER_TYPE_SELL : ORDER_TYPE_BUY ;
			request.position  = ::PositionGetInteger(POSITION_TICKET);
			request.symbol    = symbol;
			request.volume    = lots;
			request.magic     = ::PositionGetInteger(POSITION_MAGIC);
			request.deviation = (ulong)slippage;
			request.comment   = "from #" + ::IntegerToString(ticket);
	
			// filling type
			if (CFAE_TRADES::IsFillingTypeAllowed(symbol, SYMBOL_FILLING_FOK))
				request.type_filling = ORDER_FILLING_FOK;
			else if (CFAE_TRADES::IsFillingTypeAllowed(symbol, SYMBOL_FILLING_IOC))
				request.type_filling = ORDER_FILLING_IOC;
			else if (CFAE_TRADES::IsFillingTypeAllowed(symbol, ORDER_FILLING_RETURN)) // just in case
				request.type_filling = ORDER_FILLING_RETURN;
	
			int success = ::OrderSend(request, result);
	
			//-- error check --------------------------------------------------
			if (!success || (result.retcode!=TRADE_RETCODE_DONE && result.retcode!=TRADE_RETCODE_PLACED && result.retcode!=TRADE_RETCODE_DONE_PARTIAL)) {
				string errmsgpfx = "Closing trade error";
				int erraction    = CFAE_TRADES::CheckForTradingError(result.retcode, errmsgpfx);
	
				switch (erraction) {
					case 0: break;    // no error
					case 1: continue; // overcomable error
					case 2: break;    // fatal error
				}
				return false;
			}
	
			//-- finish work --------------------------------------------------
			if (result.retcode == TRADE_RETCODE_DONE || result.retcode == TRADE_RETCODE_PLACED || result.retcode == TRADE_RETCODE_DONE_PARTIAL) {
				//- closing: full
				if (lots0 == ::NormalizeDouble(result.volume, 5)) {
					while (true) {
						if (!::PositionSelectByTicket(ticket)) {
							break;
						}
	
						::Sleep(10);
					}
				}
				//- closing: partial
				else if (lots0 > ::NormalizeDouble(result.volume, 5))	{
					while (true) {
						if (::PositionSelectByTicket(ticket) && (lots0 != ::NormalizeDouble(PositionGetDouble(POSITION_VOLUME), 5))) {
							break;
						}
	
						::Sleep(10);
					}
				}
			}
	
			break;
		}
	
		::ResetLastError();
	
		return true;
	}
	
	static double OrderCommission() {
		if (CFAE_TRADES::LoadedType() == 1) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
			
			for (int index = 0; index < total; index++) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_IN) {
					return ::HistoryDealGetDouble(ticket, DEAL_COMMISSION); 
				}
			}
		}
	
		if (CFAE_TRADES::LoadedType() == 2) return 0;
	
		if (CFAE_TRADES::LoadedType() == 3) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
	
			for (int index = total -1; index >= 0; index--) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_OUT) {
					return ::HistoryDealGetDouble(ticket, DEAL_COMMISSION);
				}
			}
		}
	
		if (CFAE_TRADES::LoadedType() == 4) return 0;
		
		return 0.0;
	}
	
	static double OrderLots() {
		if (CFAE_TRADES::LoadedType() == 1) return ::PositionGetDouble(POSITION_VOLUME);
	
		if (CFAE_TRADES::LoadedType() == 2) return ::OrderGetDouble(ORDER_VOLUME_CURRENT);
	
		if (CFAE_TRADES::LoadedType() == 3) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
	
			for (int index = total -1; index >= 0; index--) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_OUT) {
					return ::HistoryDealGetDouble(ticket, DEAL_VOLUME);
				}
			}
		}
	
		if (CFAE_TRADES::LoadedType() == 4) return ::HistoryOrderGetDouble(CFAE::OrderTicket(), ORDER_VOLUME_CURRENT);
	
		return 0.0;
	}
	
	static long OrderMagicNumber() {
		if (CFAE_TRADES::LoadedType() == 1) return (long)::PositionGetInteger(POSITION_MAGIC);
	
		if (CFAE_TRADES::LoadedType() == 2) return (long)::OrderGetInteger(ORDER_MAGIC);
	
		if (CFAE_TRADES::LoadedType() == 3) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
	
			for (int index = total -1; index >= 0; index--) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_OUT) {
					return (long)::HistoryDealGetInteger(ticket, DEAL_MAGIC);
				}
			}
		}
	
		if (CFAE_TRADES::LoadedType() == 4) return (long)::HistoryOrderGetInteger(CFAE::OrderTicket(), ORDER_MAGIC);
	
		return 0;
	}
	
	static bool OrderModify(long ticket, double price, double sl, double tp, datetime expiration, color arrow_color = clrNONE) {
		bool isTrade = true;
	
		string symbol = "";
		long magic    = 0;
	
		if (::PositionSelectByTicket(ticket)) {
			symbol = ::PositionGetString(POSITION_SYMBOL);
		}
		else if (::OrderSelect(ticket)) {
			isTrade = false;
	
			symbol = ::OrderGetString(ORDER_SYMBOL);
		}
		else {
			return false;
		}
	
		::ResetLastError();
	
		//-- pre-fixing ---------------------------------------------------
		int digits = (int)::SymbolInfoInteger(symbol, SYMBOL_DIGITS);
	
		sl = ::NormalizeDouble(sl, digits);
		tp = ::NormalizeDouble(tp, digits);
		price = ::NormalizeDouble(price, digits);
	
		while (true) {
			//-- close --------------------------------------------------------
			MqlTradeRequest request;
			MqlTradeResult result;
			::ZeroMemory(request);
			::ZeroMemory(result);
	
			if (isTrade) {
				if (
					   sl == ::NormalizeDouble(PositionGetDouble(POSITION_SL), digits)
					&& tp == ::NormalizeDouble(PositionGetDouble(POSITION_TP), digits)
				) {
					return true;
				}
	
				request.action   = TRADE_ACTION_SLTP;
				request.symbol   = symbol;
				request.position = ::PositionGetInteger(POSITION_TICKET);
				request.magic    = ::PositionGetInteger(POSITION_MAGIC);
				request.comment  = ::PositionGetString(POSITION_COMMENT);
			}
			else {
				//-- check if needed to modify ------------------------------------
				if (
					   price == ::NormalizeDouble(OrderGetDouble(ORDER_PRICE_OPEN), digits)
					&& sl == ::NormalizeDouble(OrderGetDouble(ORDER_SL), digits)
					&& tp == ::NormalizeDouble(OrderGetDouble(ORDER_TP), digits)
					&& expiration == ::OrderGetInteger(ORDER_TIME_EXPIRATION)
				) {
					return true;
				}
	
				request.action   = TRADE_ACTION_MODIFY;
				request.order    = ::OrderGetInteger(ORDER_TICKET);
				request.price    = price;
				request.volume   = ::OrderGetDouble(ORDER_VOLUME_CURRENT);
				request.magic    = ::OrderGetInteger(ORDER_MAGIC);
				request.type_time  = ORDER_TIME_SPECIFIED;
				request.expiration = expiration;
				request.comment    = ::OrderGetString(ORDER_COMMENT);
	
				//-- filling type
				uint filling=(uint)::SymbolInfoInteger(request.symbol,SYMBOL_FILLING_MODE);
	
				if (filling==SYMBOL_FILLING_FOK) {
					request.type_filling=ORDER_FILLING_FOK;
				}
				else if (filling==SYMBOL_FILLING_IOC) {
					request.type_filling=ORDER_FILLING_IOC;
				}
			}
	
			request.sl = sl;
			request.tp = tp;
		
			int success = ::OrderSend(request, result);
			
			//-- error check --------------------------------------------------
			if (!success || (result.retcode!=TRADE_RETCODE_DONE && result.retcode!=TRADE_RETCODE_PLACED && result.retcode!=TRADE_RETCODE_DONE_PARTIAL)) {
				string errmsgpfx = "Modify error";
				int erraction    = CFAE_TRADES::CheckForTradingError(result.retcode, errmsgpfx);
	
				switch (erraction) {
					case 0: break;    // no error
					case 1: continue; // overcomable error
					case 2: break;    // fatal error
				}
				return false;
			}
			
			//-- finish work --------------------------------------------------
			if (result.retcode==TRADE_RETCODE_DONE || result.retcode==TRADE_RETCODE_PLACED || result.retcode==TRADE_RETCODE_DONE_PARTIAL) {
				int w;
	
				for (w = 0; w < 5000; w++) {
					double actualSl = ::NormalizeDouble(OrderStopLoss(), digits);
					double actualTp = ::NormalizeDouble(OrderTakeProfit(), digits);
	
					if (
						((CFAE_TRADES::LoadedType() == 1 && ::PositionSelectByTicket(ticket)) || ::OrderSelect(ticket))
						&& (sl == actualSl && tp == actualTp)
					) {
						break;
					}
	
					::Sleep(1);
				}
				
				if (w == 5000) {
					::Print("Check error: Modify order stops");
	
					return false;
				}
			}
			
			break;
		}
	
		::ResetLastError();
	
		return true;
	}
	
	static double OrderOpenPrice() {
		if (CFAE_TRADES::LoadedType() == 1) return ::PositionGetDouble(POSITION_PRICE_OPEN);
	
		if (CFAE_TRADES::LoadedType() == 2) return ::OrderGetDouble(ORDER_PRICE_OPEN);
	
		if (CFAE_TRADES::LoadedType() == 3) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
	
			for (int index = 0; index < total; index++) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_IN) {
					return ::HistoryDealGetDouble(ticket, DEAL_PRICE); 
				}
			}
		}
	
		if (CFAE_TRADES::LoadedType() == 4) return ::HistoryOrderGetDouble(CFAE::OrderTicket(), ORDER_PRICE_OPEN);
	
		return 0.0;
	}
	
	static datetime OrderOpenTime() {
		if (CFAE_TRADES::LoadedType() == 1) return (datetime)::PositionGetInteger(POSITION_TIME);
	
		if (CFAE_TRADES::LoadedType() == 2) return (datetime)::OrderGetInteger(ORDER_TIME_SETUP);
	
		if (CFAE_TRADES::LoadedType() == 3) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
	
			for (int index = 0; index < total; index++) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_IN) {
					return (datetime)::HistoryDealGetInteger(ticket, DEAL_TIME); 
				}
			}
		}
	
		if (CFAE_TRADES::LoadedType() == 4) return (datetime)::HistoryOrderGetInteger(CFAE::OrderTicket(), ORDER_TIME_SETUP);
	
		return 0;
	}
	
	static double OrderProfit() {
		if (CFAE_TRADES::LoadedType() == 1) return ::PositionGetDouble(POSITION_PROFIT);
	
		if (CFAE_TRADES::LoadedType() == 3) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
	
			for (int index = total -1; index >= 0; index--) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_OUT) {
					return ::HistoryDealGetDouble(ticket, DEAL_PROFIT);
				}
			}
		}
	
		return 0.0;
	}
	
	static bool OrderSelect(long index, int select, int pool = 0) {
		// SELECT_BY_POS is 0, SELECT_BY_TICKET is 1. If any other value is used, it defaults to SELECT_BY_TICKET
		// MODE_TRADES is 0, MODE_HISTORY is 1
	
		if (pool < 0 || pool > 1) pool = 0;
		if (select != 0) select = 1;
	
		bool selected = false;
		int loadedTypeTrade = 1;
		int loadedTypeOrder = 2;
	
		CFAE::OrderTicket(0);
		CFAE_TRADES::LoadedType(0);
	
		// SELECT_BY_POS
		if (select == 0) {
			// MODE_TRADES (running trades + pending orders)
			int totalTrades = 0;
			int totalOrders = 0;
	
			if (pool == 1) {
				::HistorySelect(0, ::TimeCurrent() + 1);
				
				totalTrades = ::HistoryDealsTotal();
				totalOrders = ::HistoryOrdersTotal();
				
				loadedTypeTrade = 3;
				loadedTypeOrder = 4;
			}
			else {
				totalTrades = ::PositionsTotal();
				totalOrders = ::OrdersTotal();
				
				loadedTypeTrade = 1;
				loadedTypeOrder = 2;
			}
	
			if (totalTrades == 0 && totalOrders == 0) {
				// nothing to select
				CFAE::_LastError_(ERR_INVALID_PARAMETER);
			}
			else {
				// mixed trades and orders
				int total = ::MathMax(totalTrades, totalOrders);
				int tradeIndex = 0;
				int orderIndex = 0;
				int iterationIndex = 0;
	
				while (true) {
					ulong tradeTicket = 0;
					ulong orderTicket = 0;
	
					if (tradeIndex < totalTrades) {
						if (pool == 1) {
							tradeTicket = ::HistoryDealGetTicket(tradeIndex);
	
							if (
								(tradeTicket == 0) // something is wrong
								|| (::HistoryDealGetInteger(tradeTicket, DEAL_ENTRY) != DEAL_ENTRY_OUT) // not that kind of a deal
							) {
								tradeIndex++;
								continue;
							}
	
							// However, after the OUT deal was just found, the ticket needs to be the position's ID
							if (tradeTicket > 0) {
								tradeTicket = ::HistoryDealGetInteger(tradeTicket, DEAL_POSITION_ID);
							}
						}
						else {
							tradeTicket = ::PositionGetTicket(tradeIndex);
						}
					}
	
					if (orderIndex < totalOrders) {
						if (pool == 1) {
							orderTicket            = ::HistoryOrderGetTicket(orderIndex);
							ENUM_ORDER_STATE state = (ENUM_ORDER_STATE)::HistoryOrderGetInteger(orderTicket, ORDER_STATE);
	
							if (
								(orderTicket == 0) // something is wrong
								|| (state != ORDER_STATE_CANCELED && state != ORDER_STATE_EXPIRED) // not that kind of state
							) {
								orderIndex++;
								continue;
							}
						}
						else {
							orderTicket = ::OrderGetTicket(orderIndex);
						}
					}
	
					iterationIndex++;
	
					// finished checking
					if (tradeTicket == 0 && orderTicket == 0) {
						break;
					}
					else if (tradeTicket > 0 && orderTicket == 0) {
						tradeIndex++;
						
						if (iterationIndex > index) {
							CFAE::OrderTicket(tradeTicket);
							CFAE_TRADES::LoadedType(loadedTypeTrade);
							selected = true;
							
							break;
						}
					}
					else if (tradeTicket == 0 && orderTicket > 0) {
						orderIndex++;
						
						if (iterationIndex > index) {
							CFAE::OrderTicket(orderTicket);
							CFAE_TRADES::LoadedType(loadedTypeOrder);
							selected = true;
							
							break;
						}
					}
					else if (tradeTicket <= orderTicket) {
						tradeIndex++;
						
						if (iterationIndex > index) {
							CFAE::OrderTicket(tradeTicket);
							CFAE_TRADES::LoadedType(loadedTypeTrade);
							selected = true;
							
							break;
						}
					}
					else if (tradeTicket > orderTicket) {
						orderIndex++;
						
						if (iterationIndex > index) {
							CFAE::OrderTicket(orderTicket);
							CFAE_TRADES::LoadedType(loadedTypeOrder);
							selected = true;
							
							break;
						}
					}
				}
			}
		}
		// SELECT_BY_TICKET
		else {
			long ticket = index;
	
			// Select whatever has the ticket here, the pool doesn't matter
			if (::PositionSelectByTicket(ticket)) {
				CFAE::OrderTicket(::PositionGetInteger(POSITION_IDENTIFIER));
				CFAE_TRADES::LoadedType(1);
				selected = true;
			}
			else if (::OrderSelect(ticket)) {
				CFAE::OrderTicket(ticket);
				CFAE_TRADES::LoadedType(2);
				selected = true;
			}
			else {
				::HistorySelect(0, ::TimeCurrent() + 1);
				long posID = ::HistoryDealGetInteger(ticket, DEAL_POSITION_ID);
	
				if (posID) {
					CFAE::OrderTicket(posID);
					CFAE_TRADES::LoadedType(3);
					selected = true;
				}
	
				if (selected == false) {
					long orderTicket = ::HistoryOrderGetInteger(ticket, ORDER_TICKET);
					
					if (orderTicket) {
						CFAE::OrderTicket(ticket);
						CFAE_TRADES::LoadedType(4);
						selected = true;
					}
				}
			}
		}
	
		if (selected) ::ResetLastError();
		
		return selected;
	}
	
	static int OrderSend(
		string   symbol,              // symbol 
		int      cmd,                 // operation 
		double   volume,              // volume 
		double   price,               // price 
		int      slippage,            // slippage 
		double   sl,                  // stop loss 
		double   tp,                  // take profit 
		string   comment=NULL,        // comment 
		long      magic=0,             // magic number 
		datetime expiration=0,        // pending order expiration 
		color    arrow_color=clrNONE  // color
	) {
		int type                       = cmd;
		ulong ticket                   = -1;
		bool successed                 = false;
		bool isPendingOrder            = (cmd > 1);
		ENUM_ORDER_TYPE_TIME type_time = ORDER_TIME_GTC;
	
		symbol = (symbol == NULL || symbol == "") ? ::Symbol() : symbol;
	
		if (isPendingOrder) {
			if (expiration <= 0) {
				expiration = 0;
	
				if (CFAE_TRADES::IsExpirationTypeAllowed(symbol, SYMBOL_EXPIRATION_GTC))
					type_time = ORDER_TIME_GTC;
				else
					type_time = ORDER_TIME_DAY;
			}
			else {
				type_time = ORDER_TIME_SPECIFIED;
			}
		}
		else {
			expiration = 0;
		}
	
		//-- we need this to prevent false-synchronous behaviour of MQL5 -----
		bool closing = false;
		double lots0 = 0;
		long type0   = type;
	
		if (
			   (::AccountInfoInteger(ACCOUNT_MARGIN_MODE) == ACCOUNT_MARGIN_MODE_RETAIL_NETTING)
			&& (type == POSITION_TYPE_BUY || type == POSITION_TYPE_SELL)
		) {
			if (::PositionSelect(symbol)) {
				if ((int)::PositionGetInteger(POSITION_TYPE) != type) {
					closing = true;
				}
	
				lots0 = ::NormalizeDouble(PositionGetDouble(POSITION_VOLUME), 5);
				type0 = ::PositionGetInteger(POSITION_TYPE);
			}
		}
	
		while (true) {
			// fixing
			int digits     = (int)::SymbolInfoInteger(symbol, SYMBOL_DIGITS);
			double ask     = ::SymbolInfoDouble(symbol, SYMBOL_ASK);
			double bid     = ::SymbolInfoDouble(symbol, SYMBOL_BID);
			double lotstep = ::SymbolInfoDouble(symbol, SYMBOL_VOLUME_STEP);
	
			sl     = ::NormalizeDouble(sl, digits);
			tp     = ::NormalizeDouble(tp, digits);
			price  = ::NormalizeDouble(price, digits);
			volume = ::MathFloor(volume/lotstep) * lotstep; // MQL4's OrderSend rounds to floor
	
			// MQL4 gives error 130 and doesn't make pending order when outside of the requirements listed here: https://book.mql4.com/appendix/limits
			// MQL5 seems to don't have such and instead it would make a pending order or a trade. That's why these checks are needed here.
			if (isPendingOrder) {
				if (
					(type == ORDER_TYPE_BUY_LIMIT && price >= ask)
					|| (type == ORDER_TYPE_SELL_LIMIT && price <= bid)
					|| (type == ORDER_TYPE_BUY_STOP && price <= ask)
					|| (type == ORDER_TYPE_SELL_STOP && price >= bid)
				) {
					CFAE::_LastError_(TRADE_RETCODE_INVALID_STOPS);
	
					return -1;
				}
			}
	
			// Give error 130 when the stops are wrong right away
			if (
				   ((type == POSITION_TYPE_BUY || type == ORDER_TYPE_BUY_LIMIT || type == ORDER_TYPE_BUY_STOP) && ((sl > 0 && sl >= price) || (tp > 0 && tp <= price)))
				|| ((type == POSITION_TYPE_SELL || type == ORDER_TYPE_SELL_LIMIT || type == ORDER_TYPE_SELL_STOP) && ((sl > 0 && sl <= price) || (tp > 0 && tp >= price)))
			) {
					CFAE::_LastError_(TRADE_RETCODE_INVALID_STOPS);
					return -1;
			}
	
			// send
			MqlTradeRequest request;
			MqlTradeResult result;
			MqlTradeCheckResult check_result;
			::ZeroMemory(request);
			::ZeroMemory(result);
			::ZeroMemory(check_result);
	
			request.action     = (type < 2) ? TRADE_ACTION_DEAL : TRADE_ACTION_PENDING;
			request.symbol     = symbol;
			request.volume     = volume;
			request.type       = (ENUM_ORDER_TYPE)type;
			request.price      = price;
			request.deviation  = slippage;
			request.sl         = sl;
			request.tp         = tp;
			request.comment    = comment;
			request.magic      = magic;
			request.type_time  = type_time;
			request.expiration = expiration;
	
			//-- filling type
			if (isPendingOrder) {
				if (CFAE_TRADES::IsFillingTypeAllowed(symbol, ORDER_FILLING_RETURN))
					request.type_filling = ORDER_FILLING_RETURN;
				else if (CFAE_TRADES::IsFillingTypeAllowed(symbol, ORDER_FILLING_FOK))
					request.type_filling = ORDER_FILLING_FOK;
				else if (CFAE_TRADES::IsFillingTypeAllowed(symbol, ORDER_FILLING_IOC))
					request.type_filling = ORDER_FILLING_IOC;
			}
			else {
				// in case of positions I would check for SYMBOL_FILLING_ and then set ORDER_FILLING_
				// this is because it appears that CFAE_TRADES::IsFillingTypeAllowed() works correct with SYMBOL_FILLING_, but then the position works correctly with ORDER_FILLING_
				// FOK and IOC integer values are not the same for ORDER and SYMBOL
	
				if (CFAE_TRADES::IsFillingTypeAllowed(symbol, SYMBOL_FILLING_FOK))
					request.type_filling = ORDER_FILLING_FOK;
				else if (CFAE_TRADES::IsFillingTypeAllowed(symbol, SYMBOL_FILLING_IOC))
					request.type_filling = ORDER_FILLING_IOC;
				else if (CFAE_TRADES::IsFillingTypeAllowed(symbol, ORDER_FILLING_RETURN)) // just in case
					request.type_filling = ORDER_FILLING_RETURN;
			}
	
			bool success = ::OrderSend(request, result);
	
			//-- check security flag ------------------------------------------
			if (successed == true) {
				::Print("The program will be removed because of suspicious attempt to create new positions");
				::ExpertRemove();
				::Sleep(10000);
	
				break;
			}
	
			if (success) {
				successed = true;
			}
	
			//-- error check --------------------------------------------------
			if (
				   success == false
				|| (
					   result.retcode != TRADE_RETCODE_DONE
					&& result.retcode != TRADE_RETCODE_PLACED
					&& result.retcode != TRADE_RETCODE_DONE_PARTIAL
				)
			) {
				string errmsgpfx = (type > ORDER_TYPE_SELL) ? "New pending order error" : "New position error";
	
				int erraction = CFAE_TRADES::CheckForTradingError(result.retcode, errmsgpfx);
	
				switch (erraction) {
					case 0: break;    // no error
					case 1: continue; // overcomable error
					case 2: break;    // fatal error
				}
	
				// MQL5 does not put the trading error into GetLastError, but I need it for later use in GetLastError
				CFAE::_LastError_(result.retcode);
	
				return -1;
			}
	
			//-- finish work --------------------------------------------------
			if (
				   result.retcode==TRADE_RETCODE_DONE
				|| result.retcode==TRADE_RETCODE_PLACED
				|| result.retcode==TRADE_RETCODE_DONE_PARTIAL
			) {
				ticket = result.order;
				//== Whatever was created, we need to wait until MT5 updates it's cache
	
				//-- Synchronize: Position
				if (type <= ORDER_TYPE_SELL) {
					if (::AccountInfoInteger(ACCOUNT_MARGIN_MODE) == ACCOUNT_MARGIN_MODE_RETAIL_NETTING) {
						if (closing == false) {
							//- new position: 2 situations here - new position or add to position
							//- ... because of that we will check the lot size instead of PositionSelect
							while (true) {
								if (::PositionSelect(symbol) && (lots0 != ::NormalizeDouble(PositionGetDouble(POSITION_VOLUME), 5))) {
									break;
								}
	
								Sleep(10);
							}
						}
						else {
							//- closing position: full
							if (lots0 == ::NormalizeDouble(result.volume, 5)) {
								while (true) {
									if (!::PositionSelect(symbol)) {break;}
									::Sleep(10);
								}
							}
							//- closing position: partial
							else if (lots0 > ::NormalizeDouble(result.volume, 5)) {
								while (true) {
									if (::PositionSelect(symbol) && (lots0 != ::NormalizeDouble(PositionGetDouble(POSITION_VOLUME), 5))) {
										break;
									}
	
									::Sleep(10);
								}
							}
							//-- position reverse
							else if (lots0 < ::NormalizeDouble(result.volume, 5)) {
								while (true) {
									if (::PositionSelect(symbol) && (type0 != ::PositionGetInteger(POSITION_TYPE))) {
										break;
									}
	
									::Sleep(10);
								}
							}
						}
					}
					else if (::AccountInfoInteger(ACCOUNT_MARGIN_MODE) == ACCOUNT_MARGIN_MODE_RETAIL_HEDGING) {
						if (closing == false) {
							while (true) {
								if (::PositionSelectByTicket(ticket)) {
									break;
								}
	
								::Sleep(10);
							}
						}
					}
				}
				//-- Synchronize: Order
				else {
					while (true) {
						if (CFAE_TRADES::LoadPendingOrder(result.order)) {
							break;
						}
	
						::Sleep(10);
					}
				}
			}
	
			break;
		}
	
		if (ticket > 0) {
			// In MQL4 OrderSend() selects the order
			int loadedType = (isPendingOrder) ? 2 : 1; // 1 for trade, 2 for pending order
			CFAE::OrderTicket(ticket);
			CFAE_TRADES::LoadedType(loadedType);
			::ResetLastError();
		}
	
		return (int)ticket;
	}
	
	static double OrderStopLoss() {
		if (CFAE_TRADES::LoadedType() == 1) return ::PositionGetDouble(POSITION_SL);
	
		if (CFAE_TRADES::LoadedType() == 2) return ::OrderGetDouble(ORDER_SL);
	
		if (CFAE_TRADES::LoadedType() == 3) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
	
			for (int index = total -1; index >= 0; index--) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_IN) {
					ulong orderTicket = ::HistoryDealGetInteger(ticket, DEAL_ORDER);
					return ::HistoryOrderGetDouble(orderTicket, ORDER_SL); 
				}
			}
		}
	
		if (CFAE_TRADES::LoadedType() == 4) return ::HistoryOrderGetDouble(CFAE::OrderTicket(), ORDER_SL);
	
		return 0.0;
	}
	
	static double OrderSwap() {
		if (FXD_SELECTED_TYPE == 1) return ::PositionGetDouble(POSITION_SWAP);
	
		if (FXD_SELECTED_TYPE == 3) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
	
			for (int index = total -1; index >= 0; index--) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_OUT) {
					return ::HistoryDealGetDouble(ticket, DEAL_SWAP);
				}
			}
		}
	
		return 0.0;
	}
	
	static string OrderSymbol() {
		if (CFAE_TRADES::LoadedType() == 1) return ::PositionGetString(POSITION_SYMBOL);
	
		if (CFAE_TRADES::LoadedType() == 2) return ::OrderGetString(ORDER_SYMBOL);
	
		if (CFAE_TRADES::LoadedType() == 3) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
			
			for (int index = 0; index < total; index++) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_IN) {
					return ::HistoryDealGetString(ticket, DEAL_SYMBOL); 
				}
			}
		}
	
		if (CFAE_TRADES::LoadedType() == 4) return ::HistoryOrderGetString(CFAE::OrderTicket(), ORDER_SYMBOL);
	
		return _Symbol;
	}
	
	static double OrderTakeProfit() {
		if (CFAE_TRADES::LoadedType() == 1) return ::PositionGetDouble(POSITION_TP);
	
		if (CFAE_TRADES::LoadedType() == 2) return ::OrderGetDouble(ORDER_TP);
	
		if (CFAE_TRADES::LoadedType() == 3) {
			::HistorySelectByPosition(CFAE::OrderTicket());
			int total = ::HistoryDealsTotal();
	
			for (int index = total -1; index >= 0; index--) {
				ulong ticket = ::HistoryDealGetTicket(index);
				ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)::HistoryDealGetInteger(ticket, DEAL_ENTRY);
	
				if (entry == DEAL_ENTRY_IN) {
					ulong orderTicket = ::HistoryDealGetInteger(ticket, DEAL_ORDER);
					return ::HistoryOrderGetDouble(orderTicket, ORDER_TP); 
				}
			}
		}
	
		if (CFAE_TRADES::LoadedType() == 4) return ::HistoryOrderGetDouble(CFAE::OrderTicket(), ORDER_TP);
	
		return 0.0;
	}
	
	static int OrderTicket(long ticket = 0) {
		static int memory = 0;
	
		if (ticket > 0) {
			memory = (int)ticket;
		}
	
		return memory;
	}
	
	static int OrderType() {
		if (CFAE_TRADES::LoadedType() == 1) return (int)::PositionGetInteger(POSITION_TYPE);
		if (CFAE_TRADES::LoadedType() == 2) return (int)::OrderGetInteger(ORDER_TYPE);
		if (CFAE_TRADES::LoadedType() == 3) return (int)::HistoryDealGetInteger(CFAE::OrderTicket(), DEAL_TYPE);
		if (CFAE_TRADES::LoadedType() == 4) return (int)::HistoryOrderGetInteger(CFAE::OrderTicket(), ORDER_TYPE);
		
		return 0; // MQL4 returns 0 if there is nothing loaded
	}
	
	static int OrdersTotal() {
		return ::PositionsTotal() + ::OrdersTotal();
	}
	
	/**
	* Refresh the data in the predefined variables and series arrays
	* In MQL5 this function should run on every tick or calculate
	*
	* Note that when Symbol or Timeframe is changed,
	* the global arrays (Ask, Bid...) are reset to size 0,
	* and also the static variables are reset to initial values.
	*/
	static bool RefreshRates() {
		static bool initialized = false;
		static double prevAsk   = 0.0;
		static double prevBid   = 0.0;
		static int prevBars     = 0;
		static MqlRates ratesArray[1];
	
		bool isDataUpdated = false;
	
		if (initialized == false) {
			::ArraySetAsSeries(::Close, true);
			::ArraySetAsSeries(::High, true);
			::ArraySetAsSeries(::Low, true);
			::ArraySetAsSeries(::Open, true);
			::ArraySetAsSeries(::Volume, true);
	
			initialized = true;
		}
	
		// For Bars below, if the symbol parameter is provided through a string variable, the function returns 0 immediately when the terminal is started
		::Bars = ::Bars(::_Symbol, PERIOD_CURRENT);
		::Ask  = ::SymbolInfoDouble(::_Symbol, SYMBOL_ASK);
		::Bid  = ::SymbolInfoDouble(::_Symbol, SYMBOL_BID);
	
		if ((::Bars > 0) && (::Bars > prevBars)) {
			// Tried to resize these arrays below on every successful single result, but turns out that this is veeeery slow
			::ArrayResize(::Time, ::Bars);
			::ArrayResize(::Open, ::Bars);
			::ArrayResize(::High, ::Bars);
			::ArrayResize(::Low, ::Bars);
			::ArrayResize(::Close, ::Bars);
			::ArrayResize(::Volume, ::Bars);
	
			// Fill the missing data
			for (int i = prevBars; i < ::Bars; i++) {
				int success = ::CopyRates(::_Symbol, PERIOD_CURRENT, i, 1, ratesArray);
	
				if (success == 1) {
					::Time[i]   = ratesArray[0].time;
					::Open[i]   = ratesArray[0].open;
					::High[i]   = ratesArray[0].high;
					::Low[i]    = ratesArray[0].low;
					::Close[i]  = ratesArray[0].close;
					::Volume[i] = ratesArray[0].tick_volume;
				}
			}
		}
		else {
			// Update the current bar only
			int success = ::CopyRates(::_Symbol, PERIOD_CURRENT, 0, 1, ratesArray);
	
			if (success == 1) {
				::Time[0]   = ratesArray[0].time;
				::Open[0]   = ratesArray[0].open;
				::High[0]   = ratesArray[0].high;
				::Low[0]    = ratesArray[0].low;
				::Close[0]  = ratesArray[0].close;
				::Volume[0] = ratesArray[0].tick_volume;
			}
		}
	
		if (::Bars != prevBars || ::Ask != prevAsk || ::Bid != prevBid) {
			isDataUpdated = true;
		}
	
		prevBars = ::Bars;
		prevAsk  = ::Ask;
		prevBid  = ::Bid;
	
		return isDataUpdated;
	}
	
	/**
	* In MQL5 when length is 0, it returns an empty string
	* In MQL4 when length is 0, it returns the whole string
	*/
	static string StringSubstr(const string string_value, int start_pos, int length = 0) {
		return ::StringSubstr(string_value, start_pos, ((length <= 0) ? -1 : length));
	}
	
	static string StringTrimLeft(string string_var) {
		::StringTrimLeft(string_var);
	
		return string_var;
	}
	
	static string StringTrimRight(string string_var) {
		::StringTrimRight(string_var);
	
		return string_var;
	}
	
	static int TimeDay(datetime date) {
		MqlDateTime tm;
		::TimeToStruct(date,tm);
	
		return tm.day;
	}
	
	static int TimeDayOfWeek(datetime date) {
		MqlDateTime tm;
		::TimeToStruct(date,tm);
	
		return tm.day_of_week;
	}
	
	static int TimeHour(datetime date) {
		MqlDateTime tm;
		::TimeToStruct(date,tm);
	
		return tm.hour;
	}
	
	static int TimeMinute(datetime date) {
		MqlDateTime tm;
		::TimeToStruct(date,tm);
	
		return tm.min;
	}
	
	static int TimeMonth(datetime date) {
		MqlDateTime tm;
		::TimeToStruct(date,tm);
	
		return tm.mon;
	}
	
	static int TimeYear(datetime date) {
		MqlDateTime tm;
		::TimeToStruct(date,tm);
	
		return tm.year;
	}
	
	/**
	* Values in ENUM_APPLIED_PRICE are from 0 to 6 in MQL4 and from 1 to 7 in MQL5.
	* These overloads help with the situation when the applied price is privided as an integer value.
	*/
	static ENUM_APPLIED_PRICE _ConvertAppliedPrice_(ENUM_APPLIED_PRICE applied_price) {
		return applied_price;
	}
	
	static ENUM_APPLIED_PRICE _ConvertAppliedPrice_(int applied_price) {
		return (ENUM_APPLIED_PRICE)(++applied_price);
	}
	
	static ENUM_OBJECT_PROPERTY_INTEGER _ConvertEnumObjectPropertyInteger_(int propID) {
		// The extra "case" in some rows are the MQL5 values for the particular constant
		switch (propID) {
			case 6 : case 0 : return OBJPROP_COLOR;
			case 7 : case 1 : return OBJPROP_STYLE;
			case 8 : case 2 : return OBJPROP_WIDTH;
			case 9 : case 3 : return OBJPROP_BACK;
			case 207 :        return OBJPROP_ZORDER;
			case 1031 :       return OBJPROP_FILL;
			case 208 :        return OBJPROP_HIDDEN;
			case 4 :          return OBJPROP_SELECTED;
			case 1028 :       return OBJPROP_READONLY;
			case 18 : /*case 7 :*/    return OBJPROP_TYPE;
			case 19 : /*case 8 :*/    return OBJPROP_TIME;
			case 1000 : /*case 10 :*/ return OBJPROP_SELECTABLE;
			case 998 : /*case 11 :*/  return OBJPROP_CREATETIME;
			case 200 :             return OBJPROP_LEVELS;
			case 201 :             return OBJPROP_LEVELCOLOR;
			case 202 :             return OBJPROP_LEVELSTYLE;
			case 203 :             return OBJPROP_LEVELWIDTH;
			case 1036 :            return OBJPROP_ALIGN;
			case 100 : case 1002 : return OBJPROP_FONTSIZE;
			case 1003 :            return OBJPROP_RAY_LEFT;
			case 1004 :            return OBJPROP_RAY_RIGHT;
			case 10 : case 1032 :  return OBJPROP_RAY;
			case 11 : /*case 1005 :*/  return OBJPROP_ELLIPSE;
			case 14 : /*case 1008 :*/  return OBJPROP_ARROWCODE;
			case 15 : /*case 12 :*/    return OBJPROP_TIMEFRAMES;
			case 1011 :                  return OBJPROP_ANCHOR;
			case 102 : /*case 1012 :*/ return OBJPROP_XDISTANCE;
			case 103 : /*case 1013 :*/ return OBJPROP_YDISTANCE;
			case 1014 : return OBJPROP_DIRECTION;
			case 1015 : return OBJPROP_DEGREE;
			case 1016 : return OBJPROP_DRAWLINES;
			case 1018 : return OBJPROP_STATE;
			case 1030 : return OBJPROP_CHART_ID;
			case 1019 : return OBJPROP_XSIZE;
			case 1020 : return OBJPROP_YSIZE;
			case 1033 : return OBJPROP_XOFFSET;
			case 1034 : return OBJPROP_YOFFSET;
			case 1022 : return OBJPROP_PERIOD;
			case 1023 : return OBJPROP_DATE_SCALE;
			case 1024 : return OBJPROP_PRICE_SCALE;
			case 1027 : return OBJPROP_CHART_SCALE;
			case 1025 : return OBJPROP_BGCOLOR;
			case 101 : /*case 1026 :*/ return OBJPROP_CORNER;
			case 1029 : return OBJPROP_BORDER_TYPE;
			case 1035 : return OBJPROP_BORDER_COLOR;
		}
	
		return (ENUM_OBJECT_PROPERTY_INTEGER)-1;
	}
	
	
	static ENUM_OBJECT_PROPERTY_STRING _ConvertEnumObjectPropertyString_(int propID) {
		// The extra "case" in some rows are the MQL5 values for the particular constant
		switch (propID) {
			case 1037 : case 5 : return OBJPROP_NAME;
			case 999 : case 6 :  return OBJPROP_TEXT;
			case 206 :           return OBJPROP_TOOLTIP;
			case 205 :           return OBJPROP_LEVELTEXT;
			case 1001 :          return OBJPROP_FONT;
			case 1017 :          return OBJPROP_BMPFILE;
			case 1021 :          return OBJPROP_SYMBOL;
		}
	
		return (ENUM_OBJECT_PROPERTY_STRING)-1;
	}
	
	/**
	* In MQL4 the values are the number of minutes in the period
	* In MQL5 the values are the minutes up to M30, then it's the number of seconds in the period
	* This function converts all values that exist in MQL4, but not in MQL5
	* There are no conflict values otherwise
	*/
	static ENUM_TIMEFRAMES _ConvertTimeframe_(int timeframe) {
		switch (timeframe) {
			case 60    : return PERIOD_H1;
			case 120   : return PERIOD_H2;
			case 180   : return PERIOD_H3;
			case 240   : return PERIOD_H4;
			case 360   : return PERIOD_H6;
			case 480   : return PERIOD_H8;
			case 720   : return PERIOD_H12;
			case 1440  : return PERIOD_D1;
			case 10080 : return PERIOD_W1;
			case 43200 : return PERIOD_MN1;
		}
	
		return (ENUM_TIMEFRAMES)timeframe;
	}
	static ENUM_TIMEFRAMES _ConvertTimeframe_(ENUM_TIMEFRAMES timeframe) {
		return timeframe;
	}
	
	static double _GetIndicatorValue_(int handle, int mode = 0, int shift = 0, bool isCustom = false) {
		static double buffer[1];
	
		double valueOnError = (isCustom) ? EMPTY_VALUE : 0.0;
	
		::ResetLastError(); 
	
		if (handle < 0) {
			::Print("Error: Indicator not loaded (handle=", handle, " | error code=", ::_LastError, ")");
	
			return valueOnError;
		}
		
		int barsCalculated = 0;
	
		for (int i = 0; i < 100; i++) {
			barsCalculated = ::BarsCalculated(handle);
	
			if (barsCalculated > 0) break;
	
			::Sleep(50); // doesn't work when in custom indicators
		}
	
		int copied = ::CopyBuffer(handle, mode, shift, 1, buffer);
	
		// Some indicators like MA could be working fine for most candles, but not for the few oldest candles where MA cannot be calculated.
		// In this case the amount of copied idems is 0. That's why don't rely on that value and use BarsCalculated instead.
		if (barsCalculated > 0) {
			double value = (copied > 0) ? buffer[0] : EMPTY_VALUE;
			
			// In MQL4 all built-in indicators return 0.0 when they have nothing to return, for example when asked for value from non existent bar.
			// In MQL5 they return EMPTY_VALUE in this case. That's why here this fix is needed.
			if (value == EMPTY_VALUE && isCustom == false) value = 0.0;
			
			return value;
		}
	
		CFAE::_IndicatorProblem_(true);
	
		return valueOnError;
	}
	
	/**
	* _IndicatorProblem_() to get the state
	* _IndicatorProblem_(true) or _IndicatorProblem_(false) to set the state
	*/
	static bool _IndicatorProblem_(int setState = -1) {
		static bool memory = false;
	
		if (setState > -1) memory = setState;
	
		if (memory == 1) FXD_INDICATOR_COUNTED_MEMORY = 0; // Resets the IndicatorCount() function
	
		return memory;
	}
	
	/**
	* Getter
	*/
	static int _LastError_() {
		return _LastError;
	}
	/**
	* Setter
	*/
	static void _LastError_(int error) {
		_LastError = error;
	}
	
	static double iATR( 
		string symbol,
		int timeframe,
		int ma_period,
		int shift
	) {
		return CFAE::_GetIndicatorValue_(
			::iATR(
				symbol,
				CFAE::_ConvertTimeframe_(timeframe),
				ma_period),
			0,
			shift
		);
	}
	
	/**
	* Overload for the case when numeric value is used for timeframe
	*/
	static int iBarShift(const string symbol, int timeframe, datetime time, bool exact = false) {
		return ::iBarShift(symbol, CFAE::_ConvertTimeframe_(timeframe), time, exact);
	}
	
	/**
	* Overload for the case when numeric value is used for timeframe
	*/
	static long iBars(const string symbol, int timeframe) {
		return ::iBars(symbol, CFAE::_ConvertTimeframe_(timeframe));
	}
	
	/**
	* Overload for the case when numeric value is used for timeframe
	*/
	static double iClose(const string symbol, int timeframe, int shift) {
		return ::iClose(symbol, CFAE::_ConvertTimeframe_(timeframe), shift);
	}
	
	/**
	* Overload for the case when numeric value is used for timeframe
	*/
	static double iHigh(const string symbol, int timeframe, int shift) {
		return ::iHigh(symbol, CFAE::_ConvertTimeframe_(timeframe), shift);
	}
	
	/**
	* Overload for the case when numeric value is used for timeframe
	* ENUM_SERIESMODE constants are the same in both, MQL4 and MQL5
	*/
	static int iHighest(const string symbol, int timeframe, int type, int count = 0, int start = 0) {
		return ::iHighest(symbol, CFAE::_ConvertTimeframe_(timeframe), (ENUM_SERIESMODE)type, ((count == 0) ? WHOLE_ARRAY : count), start);
	}
	
	/**
	* Overload for the case when numeric value is used for timeframe
	*/
	static double iLow(const string symbol, int timeframe, int shift) {
		return ::iLow(symbol, CFAE::_ConvertTimeframe_(timeframe), shift);
	}
	
	/**
	* Overload for the case when numeric value is used for timeframe
	* ENUM_SERIESMODE constants are the same in both, MQL4 and MQL5
	*/
	static int iLowest(const string symbol, int timeframe, int type, int count = 0, int start = 0) {
		return ::iLowest(symbol, CFAE::_ConvertTimeframe_(timeframe), (ENUM_SERIESMODE)type, ((count == 0) ? WHOLE_ARRAY : count), start);
	}
	
	template<typename AP>
	static double iMA( 
		string symbol,
		int timeframe,
		int ma_period,
		int ma_shift,
		ENUM_MA_METHOD ma_method,
		AP applied_price,
		int shift
	) {
		return CFAE::_GetIndicatorValue_(
			::iMA(
				symbol,
				CFAE::_ConvertTimeframe_(timeframe),
				ma_period,
				ma_shift,
				ma_method,
				CFAE::_ConvertAppliedPrice_(applied_price)),
			0,
			shift
		);
	}
	
	/**
	* Overload for the case when numeric value is used for timeframe
	*/
	static double iOpen(const string symbol, int timeframe, int shift) {
		return ::iOpen(symbol, CFAE::_ConvertTimeframe_(timeframe), shift);
	}
	
	template<typename AP>
	static double iRSI( 
		string symbol,
		int timeframe,
		int period,
		AP applied_price,
		int shift
	) {
		return CFAE::_GetIndicatorValue_(
			::iRSI(
				symbol,
				CFAE::_ConvertTimeframe_(timeframe),
				period,
				CFAE::_ConvertAppliedPrice_(applied_price)),
			0,
			shift
		);
	}
	
	template<typename AP>
	static double iStdDev( 
		string symbol,
		int timeframe,
		int ma_period,
		int ma_shift,
		ENUM_MA_METHOD ma_method,
		AP applied_price,
		int shift
	)
	{
		return CFAE::_GetIndicatorValue_(
			::iStdDev(
				symbol,
				CFAE::_ConvertTimeframe_(timeframe),
				ma_period,
				ma_shift,
				ma_method,
				CFAE::_ConvertAppliedPrice_(applied_price)),
			0,
			shift
		);
	}
	
	/**
	* Overload for the case when numeric value is used for timeframe
	*/
	static datetime iTime(const string symbol, int timeframe, int shift) {
		return ::iTime(symbol, CFAE::_ConvertTimeframe_(timeframe), shift);
	}
};
int CFAE::_LastError = -1;

class CFAE_TRADES
{
public:
	/**
	* Constructor
	*/
	CFAE_TRADES() {};
	
		static int CheckForTradingError(int error_code = -1, string msg_prefix = "")
		{
			// return 0 -> no error
			// return 1 -> overcomable error
			// return 2 -> fatal error
	
			static int tryout = 0;
			int tryouts = 5;   // How many times to retry
			int delay   = 1000; // Time delay between retries, in milliseconds
			int retval  = 0;
	
			//-- error check -----------------------------------------------------
			switch(error_code)
			{
				//-- no error
				case 0:
					retval = 0;
					break;
				//-- overcomable errors
				case TRADE_RETCODE_REQUOTE:
				case TRADE_RETCODE_REJECT:
				case TRADE_RETCODE_ERROR:
				case TRADE_RETCODE_TIMEOUT:
				case TRADE_RETCODE_INVALID_VOLUME:
				case TRADE_RETCODE_INVALID_PRICE:
				case TRADE_RETCODE_INVALID_STOPS:
				case TRADE_RETCODE_INVALID_EXPIRATION:
				case TRADE_RETCODE_PRICE_CHANGED:
				case TRADE_RETCODE_PRICE_OFF:
				case TRADE_RETCODE_TOO_MANY_REQUESTS:
				case TRADE_RETCODE_NO_CHANGES:
				case TRADE_RETCODE_CONNECTION:
					retval = 1;
					break;
				//-- critical errors
				default:
					retval = 2;
					break;
			}
	
			if (error_code > 0)
			{
				if (retval == 1)
				{
					Print(msg_prefix,": ",(error_code),". Retrying in ",(delay)," milliseconds..");
					Sleep(delay); 
				}
				else if (retval == 2)
				{
					Print(msg_prefix,": ",(error_code));
				}
			}
	
			if (retval == 0)
			{
				tryout = 0;
			}
			else if (retval == 1)
			{
				tryout++;
	
				if (tryout > tryouts)
				{
					tryout = 0;
					retval  = 2;
				}
				else
				{
					Print("retry #", tryout, " of ", tryouts);
				}
			}
	
			return retval;
		}
	
		static bool IsExpirationTypeAllowed(string symbol, int exp_type)
		{
			int expiration = (int)SymbolInfoInteger(symbol,SYMBOL_EXPIRATION_MODE);
			return ((expiration&exp_type) == exp_type);
		}
	
		static bool IsFillingTypeAllowed(string symbol,int fill_type)
		{
			int filling=(int)SymbolInfoInteger(symbol,SYMBOL_FILLING_MODE);
			return((filling & fill_type)==fill_type);
		}
	
	static bool LoadPendingOrder(long ticket)
	{
		bool success = false;
	
	   if (::OrderSelect(ticket))
		{
			// The order could be from any type, so check the type
			// and allow only true pending orders.
			ENUM_ORDER_TYPE type = (ENUM_ORDER_TYPE)::OrderGetInteger(ORDER_TYPE);
	
			if (
				   type == ORDER_TYPE_BUY_LIMIT
				|| type == ORDER_TYPE_SELL_LIMIT
				|| type == ORDER_TYPE_BUY_STOP
				|| type == ORDER_TYPE_SELL_STOP
			) {
				CFAE_TRADES::LoadedType(2);
				CFAE::OrderTicket(ticket);
				success = true;
			}
		}
	
	   return success;
	}
	
	static int LoadedType(int type = 0)
	{
		// 1 - position
		// 2 - pending order
		// 3 - history position
		// 4 - history pending order
	
		static int memory;
	
		if (type > 0) {memory = type;}
	
		return memory;
	}
};
bool ___RefreshRates___ = CFAE::RefreshRates();

//== WAKA MQL5 ==//
