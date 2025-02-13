# IO mapping for BaseIntefaceUa

## Principle
The cltrX Core has an OPC UA Server, *but no OPC UA Client*.

The Siemens S7 has both client AND server.

That's why we use the client on S7 side and the server on S7 side.

### CtrlX Core provides the server
CtrlX do not launch any action.

### Siemens S7 is the client
S7 reads data from the server.

S7 write data to the server.

The client S7 read and write data from/to the ctrlX as if there was I/O Tags.
The client S7 cannot read/write on structure. That's why the communication is done with simple type on ctrlX side.

# All PLC Tags in ctrlX as OPC UA Server

|Siemens Hw|Data Type| ctrlX Tag                    | ctrlX direction|
|----------|---------|------------------------------|----------------|
|          |BOOL     |UA_ButtonAndSignal_In_Estop   | Input          |
|          |BOOL     |UA_ButtonAndSignal_In_Reset   | Input          |
|          |BOOL     |UA_ButtonAndSignal_In_Start   | Input          |
|          |BOOL     |UA_ButtonAndSignal_In_Stop   | Input          |
|          |REAL     |UA_Balluf_bcm0002_Data_1   | Input          |
|          |REAL     |UA_Balluf_bcm0002_Data_1   | Input          |
|          |REAL     |UA_Balluf_bcm0002_Data_1   | Input          |
|          |DWORD    |UA_Balluf_bcm0002_Status   | Input          |
|          |REAL     |UA_Balluf_bcm0002_Temperature   | Input          |
|          |WORD    |UA_O300_DL_Value   | Input          | 
|          |BOOL     |UA_O300_DL_A   | Input          |
|          |BOOL     |UA_O300_DL_Q   | Input          |
|          |BOOL     |UA_O300_DL_BCD1   | Input          |           
|          |BOOL     |UA_O300_ZL_A   | Input          |
|          |BOOL     |UA_O300_ZL_Q   | Input          |
|          |BOOL     |UA_O300_ZL_BCD1   | Input          |
|          |WORD     |UA_U300_D50_Value   | Input          |
|          |BOOL     |UA_U300_D50_A   | Input          |
|          |BOOL     |UA_U300_D50_Q   | Input          |
|          |SINT     |UA_U300_D50_Scale   | Input          |
|          |BOOL     |UA_U300_D50_SSC1   | Input          |
|          |BOOL     |UA_U300_D50_SSC2   | Input          |
|          |BOOL     |UA_U300_D50_SSC4   | Input          |
|          |DWORD    |UA_U300_P50_Value   | Input          |
|          |BOOL     |UA_U300_P50_A   | Input          |
|          |BOOL     |UA_U300_P50_Q   | Input          |
|          |SINT     |UA_U300_P50_Scale   | Input          |
|          |BOOL     |UA_U300_P50_SSC1   | Input          |
|          |BOOL     |UA_U300_P50_SSC2   | Input          |
|          |BOOL     |UA_U300_P50_SSC4               | Input          |
|          |WORD     |UA_Schunk_mms_Value            | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_0_0   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_0_1   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_0_2   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_0_3   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_0_4   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_0_5   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_0_6   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_0_7   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_1_0   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_1_1   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_1_2   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_1_3   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_1_4   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_1_5   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_1_6   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_1_7   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_2_0   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_2_1   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_2_2   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_2_3   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_2_4   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_2_5   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_2_6   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_2_7   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_3_0   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_3_1   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_3_2   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_3_3   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_3_4   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_3_5   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_3_6   | Input          |
|          |BOOL     |UA_DigitalInput_32_Input_3_7   | Input          |
|----------|---------|------------------------------|----------------|    
|          |BOOL     |UA_ButtonAndSignal_Out_Execute| Output |
|          |BOOL     |UA_ButtonAndSignal_Out_Idle| Output |
|          |BOOL     |UA_ButtonAndSignal_Out_Stopped| Output |
|          |BOOL     |UA_Festo_SetOut| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_0_0| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_0_1| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_0_2| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_0_3| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_0_4| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_0_5| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_0_6| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_0_7| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_1_0| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_1_1| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_1_2| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_1_3| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_1_4| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_1_5| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_1_6| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_1_7| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_2_0| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_2_1| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_2_2| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_2_3| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_2_4| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_2_5| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_2_6| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_2_7| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_3_0| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_3_1| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_3_2| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_3_3| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_3_4| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_3_5| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_3_6| Output |
|          |BOOL     |UA_DigitalOutput_32_Output_3_7| Output |
