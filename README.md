

# Background-Removal plugin for ImageJ and ImageJ2 (Fiji) 
ImageJ is a fully java-based software for image processing in fields such as physics and biology. Our plugin aims to remove the background from a stack of images using the Low Rank + Sparse + Noise method from the article [Greedy Bilateral Sketch, Completion & Smoothing](https://proceedings.mlr.press/v31/zhou13b.html) and inspired by the [Python code of the GreGoDec algorithm](https://github.com/FattaccioliLab/Codes/tree/master/LowRankSparseNoiseDecomposition-GoDec). The original Matlab code from [Tianyi Zhou](https://tianyizhou.github.io/) has been forked by Andrews Sobral [here](https://github.com/andrewssobral/lrslibrary/blob/master/algorithms/rpca/GreGoDec/GreGoDec.m).

* Low Rank => Background matrix
* Sparse => Moving objects martrix
* Noise => Disruption and errors matrix

## Example of Low Rank + Sparse + Noise method
**Original images:** | **Background images:** | **Sparse images:** | **Noise:**
--- | --- | --- | ---
![Original](/samples/gifs/1-Original.gif) | ![Background](/samples/gifs/2-Background.gif) | ![Sparse](/samples/gifs/3-Sparse.gif) | ![Noise](/samples/gifs/4-Noise_1.gif)

## Installation tutorial
###### Requirement:  [ImageJ (Fiji)](https://imagej.net/software/fiji/downloads) / Apache Maven and Java

### Directly installing the .jar file as plugin in ImageJ

You can get the `.jar` of this plugin from the plugins folder [here](https://sites.imagej.net/FattaccioliLab/). 

### From the dedicated Fiji update site

You can add our update site [[here](https://sites.imagej.net/FattaccioliLab/)](https://sites.imagej.net/FattaccioliLab/) to the Fiji Updater, following this tutorial : [https://imagej.net/update-sites/following](https://imagej.net/update-sites/following)

### Using Maven

From the project folder with Maven :
```bash
cd  Background-Removal-Plugin---ImageJ
```
```bash
mvn clean package -Denforcer.skip=true
```
```bash
cd  target
```
The file is named `BackgroundRemoval-0.1.0-SNAPSHOT.jar` in the project folder and `GreGoDec-v0.1.jar` in the ImageJ website. After you get the .jar plugin, you just need to paste it into plugins Fiji.app folder.

## How to use it ?
You should now see `Background Removal` in the Fiji `Plugins` bar:  
<p align="center">
	<img src="/samples/gifs/ImageJ_1.png" width="350" height="450">  
</p>  
After clicking, the GUI appears, you can select a file with the associated button (opens the same files as Fiji) and swipe to see all frames:   
<p align="center">
  <img src="/samples/gifs/select_file.gif">
</p>  

* The gray clock changes color depending on the estimated time needed to `Finalize` the calculation, **approximately** for default parameters:
	*  🟢 **Green clock** < 5 seconds.
	*  🟠 **Orange clock** < 20 seconds.
	*  🔴 **Red clock** >= 20 seconds.  

Parameters like `Rank`, `Power`, `Error tolerance`, `Thresholding mode`, `Tau` and `k` (numbers of greatest singular values in the SVD calculation)  can be chosen to influence the output. You can choose `Preview` to see the result for the first 100 frames (or less if the stack has less frames):
<p align="center">
  <img src="/samples/gifs/Preview.gif">
</p>     

If the output preview is satisfactory, you can choose to `Finalize` and save it from the default Fiji GUI:
<p align="center">
  <img src="/samples/gifs/Finalize.gif">
</p>     

## Credits

v0.1 : 2022 - 2023 : Lyes LAÏMOUCHE,  Alina NOVIKOVA, Daniel SIMA (Master in [Software Science and Technology (STL)](https://sciences.sorbonne-universite.fr/en/formation-sciences/masters/master-informatique/parcours-stl) at Sorbonne Université, First year project) 
