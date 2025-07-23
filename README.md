# Pizza Oven Project Using TwinCAT 3

A simple PLC program demonstrating a state-machine–driven pizza oven with realtime visuals.

## States

Defined in `PizzaOven/PLC1/DUTs/E_PizzaOvenStates.TcDUT`  
1. WaitForPizzaInOven  
2. WeJustGotAPizza  
3. MovePizzaOutOfOven  
4. MovePizzaToTray  

## Code Flow

1. WaitForPizzaInOven  
   • Visual prompts “Insert Pizza.”  
   • On Insert-Pizza button, `bLoadPizza` → WeJustGotAPizza.  

2. WeJustGotAPizza  
   • Move pizza into oven, start 4 s `TON` timer.  
   • When timer finishes → MovePizzaOutOfOven.  

3. MovePizzaOutOfOven  
   • If 'bPizzaDone' = FALSE: does not eject pizza, once 'bPizzaDone' set  to TRUE, 
	 reset buzzer → MovePizzaToTray.  
	 
   • Else (timer expired): turn on buzzer & display “Pizza Is Burning.”  

4. MovePizzaToTray  
   • Increment `nTotalPizzasCooked`.  
   • Reset flags → back to WaitForPizzaInOven.  

## Visualization

- `sCurrentStateString` shows the current state on your visual screen  
- Buttons: Insert Pizza, Pack Pizza  
- Indicators: oven door, buzzer, lights  

## How to Run

1. Open `PizzaOven.tsproj` in VS with TwinCAT 3.  
2. Build & download to your PLC.  
3. Launch the visualization runtime to operate the oven.