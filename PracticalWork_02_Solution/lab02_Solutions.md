<h1 align="center">
  <br>
  <img src="./img/hei-en.png" alt="HEI-Vs Logo" width="350">
  <br>
  HEI-Vs Engineering School - Industrial Automation Base
  <br>
</h1>

Cours AutB

Author: [Cédric Lenoir](mailto:cedric.lenoir@hevs.ch)

# LAB-02-AutB-Data-Structure Solutions

## ST_Conveyor
```iecst
(*
	www.hevs.ch
	Institut Systemes Industriels
	Project: 	Projet No: PW_02
	Author:		Cedric Lenoir
	Date:		2024 January 16
	
	Summary:	Main structure for conveyor.
*)
TYPE ST_Conveyor :
STRUCT
	cm01	: ST_StationConveyor;
	cm02	: ST_StationConveyor;
	cm03	: ST_StationConveyor;
	cmOut	: ST_OutputConveyor;
	cmDrive	: ST_MotorConveyor;
END_STRUCT
END_TYPE
```

## ST_StationConveyor
```iecst
(*
	www.hevs.ch
	Institut Systemes Industriels
	Project: 	Projet No: PW_02
	Author:		Cedric Lenoir
	Date:		2023 October 11
	
	Summary:	List of of components for a station of a conveyor.
*)
TYPE ST_StationConveyor :
STRUCT
	bButton	: BOOL;
	bLed    : BOOL;
	bSensor : BOOL;
END_STRUCT
END_TYPE
```

## ST_OutputConveyor
```iecst
(*
	www.hevs.ch
	Institut Systemes Industriels
	Project: 	Projet No: PW_02
	Author:		Cedric Lenoir
	Date:		2024 January 14
	
	Summary:	ST_OutputConveyor extends ST_StationConveyor.
*)
TYPE ST_OutputConveyor EXTENDS ST_StationConveyor :
STRUCT
	bBuzzer		: BOOL;
END_STRUCT
END_TYPE
```

## ST_MotorConveyor
```iecst
(*
	www.hevs.ch
	Institut Systemes Industriels
	Project: 	Projet No: PW_02
	Author:		Cedric Lenoir
	Date:		2023 October 11
	
	Summary:	List of of components for a motor of a conveyor.
*)
TYPE ST_MotorConveyor :
STRUCT
	bK_ActivatePositiveDirection	: BOOL;
	bK_ActivateNegativeDirection	: BOOL;
END_STRUCT
END_TYPE
```

## FB_Station
```iecst
(*
	www.hevs.ch
	Institut Systemes Industriels
	Project: 	Projet No: PW_02
	Author:		Cedric Lenoir
	Date:		2024 January 16
	
	Summary:	Manage One station for a conveyor.
*)
FUNCTION_BLOCK FB_Station
VAR_INPUT
	Enable		: BOOL;
END_VAR
VAR_IN_OUT
	ioStation	: ST_StationConveyor;
END_VAR
VAR_OUTPUT
	diCounter	: DINT;
	stop		: BOOL;
	release	    : BOOL;
END_VAR
VAR
	// Used to count the number of inputs in station
	rTrigIn		: R_TRIG;
	// Reset Counte if TON for more that 2 seconds
	tonResetCounter	: TON;
END_VAR

//
// Code
//
IF Enable THEN
	rTrigIn(CLK := ioStation.bSensor);
	
	IF rTrigIn.Q THEN
		diCounter := diCounter + 1;
		release := FALSE;
		stop := TRUE;
	END_IF
	IF ioStation.bButton THEN
		release := TRUE;
		stop := FALSE;
	END_IF
	ioStation.bLed := stop;
	
	tonResetCounter(IN := ioStation.bButton,
					PT := T#2S);
					
	IF tonResetCounter.Q THEN
		diCounter := 0;
	END_IF
END_IF
```

## FB_OutStation
```iecst
(*
	www.hevs.ch
	Institut Systemes Industriels
	Project: 	Projet No: PW_02
	Author:		Cedric Lenoir
	Date:		2024 January 16
	
	Summary:	Manage One station for a conveyor.
*)
FUNCTION_BLOCK FB_OutStation
VAR_INPUT
	Enable		: BOOL;
END_VAR
VAR_IN_OUT
	ioStation	: ST_OutputConveyor;
END_VAR
VAR_OUTPUT
	diCounter	: DINT;
	stop		: BOOL;
	release	    : BOOL;
END_VAR
VAR
	// Used to count the number of inputs in station
	rTrigIn		: R_TRIG;
	// Reset Counte if TON for more that 2 seconds
	tonResetCounter	: TON;
END_VAR

//
// Code
//
IF Enable THEN
	rTrigIn(CLK := ioStation.bSensor);
	
	IF rTrigIn.Q THEN
		diCounter := diCounter + 1;
		release := FALSE;
		stop := TRUE;
	END_IF
	IF ioStation.bButton THEN
		release := TRUE;
		stop := FALSE;
	END_IF
	ioStation.bLed := stop;
	
	tonResetCounter(IN := ioStation.bButton,
					PT := T#2S);
					
	IF tonResetCounter.Q THEN
		diCounter := 0;
	END_IF
	
	ioStation.bBuzzer := stop;
END_IF
```

## FB_Drive
```iecst
(*
	www.hevs.ch
	Institut Systemes Industriels
	Project: 	Projet No: PW_02
	Author:		Cedric Lenoir
	Date:		2024 January 16
	
	Summary:	Manage drive for motor conveyor.
*)
FUNCTION_BLOCK FB_Drive
VAR_INPUT
	Enable	: BOOL;
END_VAR
VAR_IN_OUT
	ioDrive			: ST_MotorConveyor;
	stationOne		: FB_Station;
	stationTwo		: FB_Station;
	stationThree	: FB_Station;
	stationOut		: FB_OutStation;
END_VAR
VAR_OUTPUT
END_VAR
VAR
END_VAR

//
// Code
//
IF Enable THEN
	ioDrive.bK_ActivatePositiveDirection := NOT(stationOne.stop   OR 
                                                stationTwo.stop   OR
                                                stationThree.stop OR
                                                stationOut.stop);
END_IF
```

## PLC_PRG *without in/out functions*
```iecst
(*
	www.hevs.ch
	Institut Systemes Industriels
	Project: 	Projet No: PW_02
	Author:		Cedric Lenoir
	Date:		2024 January 16
	
	Summary:	Main program for Pracatival Work 02.
*)
PROGRAM PLC_PRG
VAR
	diMyLoop		: DINT;
	emConveyor		: ST_Conveyor;
	testMode		: BOOL;
	
	fbStationOne	: FB_Station;
	fbStationTwo	: FB_Station;
	fbStationThree	: FB_Station;
	fbOutStation	: FB_OutStation;
	fbDrive			: FB_Drive;
END_VAR

//
// Code
//
diMyLoop := diMyLoop + 1;

//
// Manage inputs
//
// cm01
emConveyor.cm01.bButton := GVL_Abox.uaAboxInterface.uaDigitalIn.Input_0_0;
emConveyor.cm01.bSensor := GVL_Abox.uaAboxInterface.uaDigitalIn.Input_0_4;	//  UA_DigitalInput_32_Input_0_4;
// cm02
emConveyor.cm02.bButton := GVL_Abox.uaAboxInterface.uaDigitalIn.Input_0_1;
emConveyor.cm02.bSensor := GVL_Abox.uaAboxInterface.uaDigitalIn.Input_0_5;
// cm03
emConveyor.cm03.bButton := GVL_Abox.uaAboxInterface.uaDigitalIn.Input_0_2;
emConveyor.cm03.bSensor := GVL_Abox.uaAboxInterface.uaDigitalIn.Input_0_6;
// cmOut
emConveyor.cmOut.bButton := GVL_Abox.uaAboxInterface.uaDigitalIn.Input_0_3;
emConveyor.cmOut.bSensor := NOT GVL_Abox.uaAboxInterface.uaDigitalIn.Input_0_7;	// Signal inverted

fbStationOne(Enable := NOT testMode, 
          ioStation := emConveyor.cm01);
fbStationTwo(Enable := NOT testMode, 
          ioStation := emConveyor.cm02);
fbStationThree(Enable := NOT testMode, 
          ioStation := emConveyor.cm03);
		  
fbOutStation(Enable := NOT testMode, 
          ioStation := emConveyor.cmOut);

		  
fbDrive(Enable := NOT testMode,
		ioDrive := emConveyor.cmDrive,
        stationOne := fbStationOne,
        stationTwo := fbStationTwo,
        stationThree := fbStationThree,
        stationOut := fbOutStation);		  

//
// Manage outputs
//
// cm01
GVL_Abox.uaAboxInterface.uaDigitalOut.Output_0_0 := emConveyor.cm01.bLed;
GVL_Abox.uaAboxInterface.uaDigitalOut.Output_0_1 := emConveyor.cm02.bLed;
GVL_Abox.uaAboxInterface.uaDigitalOut.Output_0_2 := emConveyor.cm03.bLed;
GVL_Abox.uaAboxInterface.uaDigitalOut.Output_0_3 := emConveyor.cmOut.bLed;
GVL_Abox.uaAboxInterface.uaDigitalOut.Output_0_4 := emConveyor.cmDrive.bK_ActivatePositiveDirection;
GVL_Abox.uaAboxInterface.uaDigitalOut.Output_0_5 := emConveyor.cmDrive.bK_ActivateNegativeDirection;
GVL_Abox.uaAboxInterface.uaDigitalOut.Output_0_6 := emConveyor.cmOut.bBuzzer;
```

## Final code for PRG_PLC
```iecst
diMyLoop := diMyLoop + 1;

// Manage inputs
FC_GetInput(ioHwInterface := GVL_Abox,
            ioPhysicalControl := emConveyor);

// Execute Control Modules
fbStationOne(Enable := NOT testMode, 
          ioStation := emConveyor.cm01);
fbStationTwo(Enable := NOT testMode, 
          ioStation := emConveyor.cm02);
fbStationThree(Enable := NOT testMode, 
          ioStation := emConveyor.cm03);
		  
fbOutStation(Enable := NOT testMode, 
          ioStation := emConveyor.cmOut);

fbDrive(Enable := NOT testMode,
		ioDrive := emConveyor.cmDrive,
        stationOne := fbStationOne,
        stationTwo := fbStationTwo,
        stationThree := fbStationThree,
        stationOut := fbOutStation);		  

// Manage outputs
FC_SetOutput(ioHwInterface := GVL_Abox,
             ioPhysicalControl := emConveyor);
```
