# CamillaDSP-Building-a-Config-4-Get-Excess-Phase-to-Zero
4. Manipulate the phase in rePhase for each driver to get the Excess Phase close to zero.

First a plot showing the Phase and SPL, with Excess Phase highlighted.
![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm Excess Phase highlighted .jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm Excess Phase highlighted .jpg

The aim is to have the Excess Phase at 0 on the Degree scale. Bass is OK but at 330Hz the phase starts dropping, so Mid and Hi need some tweaking as shown on the Spectrogram. The strong advice with rePhase is not to alter anything under 100Hz as it will induce pre-ringing. I leave the Bass driver alone in rePhase. We will create an Excess phase version of the response in REW and export it and use rePhase to manipulate the phase and generate a filter that will make the Excess phase close to 0. Note the Phase range , -390 to +50, as we will need to enter this range into rePhase.

Here is the spectrogram 
![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm - Spectrogram.jpg>)
 REW V5.40 FS 75db EQ XO Gains Delay IPm - Spectrogram.jpg

and Impulse (Step) responses
![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm Step Response.jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm Step Response.jpg

The Impulse step response plot is not too good, yet.

We need to extract a measurement of Excess Phase from the Full System (20-20kHz) measurement and Export it for input to rePhase. We will then use the previously saved rePhase XO settings for mid and hi drivers, import the Excess Phase measurement and manipulate the phase in Rephase to get the Excess Phase close to zero. We then replace the XO filter with the new XO and PF (Phase Fix) in the Pipeline. This way there is only one rePhase generated FIR filter per channel in the pipeline, remembering that each FIR filter adds a processing delay. 

So, back to our SPL and Phase plot, right click the thumbnail and select excess phase copy

![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm generate excess phase copy.jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm generate excess phase copy.jpg

a box will pop up, click the "Make excess phase copy"
![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm box to make excess phase copy.jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm box to make excess phase copy.jpg

Locate the thumbnail on the left of the REW screen of the Excess Phase 
![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm Excess Phase copy.jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm Excess Phase copy.jpg


Click File, then "Export", then "Export measurement as text", accept the next popup 
![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm Export measurement as text.jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm Export measurement as text.jpg

and enter the file details and save the file.
![alt text](<Images/REW V5.40 FS 75db EQ XO Gains Delay IPm Export measurement as text - save.jpg>)
REW V5.40 FS 75db EQ XO Gains Delay IPm Export measurement as text - save.jpg

Reload the crossover rePhase settings for Mid and click the Paragraphic Phase EQ tab, then in the slider panel click the Presets dropdown and select "Flat 1/3 oct Mid freq" to set the slider frequencies to usable mid range values, then up the top of the screen click "File", "Import Measurement" and select the Excess Phase measurement.

 ![alt text](<Images/rePhase XO-Mid-250202-LR96-HP290Hz-LR96-LP3800Hz-4096T Import Measure.jpg>)
rePhase XO-Mid-250202-LR96-HP290Hz-LR96-LP3800Hz-4096T Import Measure.jpg

The Ranges and Measurement tabs (bottom right panel) need to be changed to get the data to display, in the Measurement tab I set gain offset to 0 to bring back the frequency response of the XO, in the Ranges tab I set the Phase at -390 to 50 corresponding to the REW measurement earlier.

Here is rePhase ready to manipulate the Excess Phase to 0 degrees
![alt text](<Images/rePhase XO-Mid-250202-LR96-HP290Hz-LR96-LP3800Hz-4096T Excess Ph Imported.jpg>)



To manipulate the phase, select a frequency, check the Excess phase amount on the Y axis and either adjust the appropriate slider to get to 0 or enter the degree into the field. Degree, Q and Frequency can be entered. When you have the phase at 0 for the measurement, enter the new filename and confirm the directory then press generate to build a .dbl file, copy it to CamillaDSP and add the new filter in the pipeline, delete the old filter if needed and re-measure. Once more the filename is a descriptor showing details of the filter and Phase Fix identifier (156 was 15 June).

It took me a few goes to get to here, but it really doesn't take long. I have learnt from bitter experience to save the settings for each iteration of the measurements as it is then simple to go back a step when you stuff up.

Here is rePhase showing the Paragraphic Phase EQ for Mid at PF3 (Phase Fix #3)
![alt text](<Images/rePhase XO-Mid-250202-LR96-HP290Hz-LR96-LP3800Hz-4096T PF3.jpg>)
rePhase XO-Mid-250202-LR96-HP290Hz-LR96-LP3800Hz-4096T PF3.jpg


RePhase for Hi showing the XO response and Excess Phase. (The ranges were altered the same as for Mid and the Presets dropdown menu set to "flat 1/3 oct high freq").
![alt text](<Images/rePhase XO-Hi-250202-LR96-HP3600Hz-4096T Excess Phase imported.jpg>)
rePhase XO-Hi-250202-LR96-HP3600Hz-4096T Excess Phase imported.jpg

Here is rePhase showing the Paragraphic Phase EQ for Hi at PF4.
![alt text](<Images/rePhase XO-Hi-250202-LR96-HP3600Hz-4096T PF4.jpg>)
rePhase XO-Hi-250202-LR96-HP3600Hz-4096T PF4.jpg

When you are satisfied with the manipulated phase, click the "generate" box and rePhase will build your FIR filter.

**********
If you are new to rePhase you can download a rePhase settings file from the rePhase Settings folder for one of the crossovers and then download the T31A XS Phase FS.txt file from the REW Measurements folder. Follow the instructions to smooth the phase.
The rePhase settings files are in the rePhase settings folder (Top of this page in the browser.) Click on the rePhase settings folder, then on the main screen, click on the .rephase file, then click on View raw, there will be a short pause then a save file dialog box will open, save the file to a folder on your computer and then open the file in rePhase - then click on a tab in the lower left pane, Linear Phase filters for the xo and Paragraphic Phase EQ for phase manipulation.
**********

The next step is to copy the XO PF files to  the CamillaDSP filters section.

Here is the CamillaDSP GUI with the Filters tab selected showing the XO filters.
![alt text](<Images/CamillaDSP GUI V3 Files tab showing dbl files.jpg>)
CamillaDSP GUI V3 Files tab showing dbl files.jpg

In this next screengrab of filters in the config, again you can see my pedantic descriptor naming of XO filters. CamillaDSP GUI, Filters tab showing FIR filters using the dbl files
![alt text](<Images/CamillaDSP GUI V3 Filters tab showing XO filters.jpg>)

So, having updated the pipeline with the new XO filters, how does it look in REW - SPL unchanged, Phase looking good,  
![alt text](<Images/REW V5.40 26 R 10_03_25 9_43 AM 11 74db no input EQ - SPL Phase.jpg>) 
REW V5.40 26 R 10_03_25 9_43 AM 11 74db no input EQ - SPL Phase.jpg

Impulse (Step Response) showing a tiny bit of pre-ringing but I think that will be inaudible
![alt text](<Images/REW V5.40 26 R 10_03_25 9_43 AM 11 74db no input EQ - Step Response.jpg>)
REW V5.40 26 R 10_03_25 9_43 AM 11 74db no input EQ - Step Response.jpg

Group Delay (GD) looks good
![alt text](<Images/REW V5.40 26 R 10_03_25 9_43 AM 11 74db no input EQ - GD.jpg>)
REW V5.40 26 R 10_03_25 9_43 AM 11 74db no input EQ - GD.jpg

and finally the Spectrogram
![alt text](<Images/REW V5.40 26 R 10_03_25 9_43 AM 11 74db no input EQ - Spectrogram.jpg>)
EW V5.40 26 R 10_03_25 9_43 AM 11 74db no input EQ - Spectrogram.jpg

The next stage is to further flatten the response by adding input PEQ filters.

https://github.com/wirrunna/CamillaDSP-Building-a-Config-5-Finishing-Touches
