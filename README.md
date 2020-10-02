# MODIS-Downscaling

**Project Title:** **Downscaling MODIS spectral bands with a deep residual encoder-decoder network**

**Authors**: Rohit Mukherjee and Desheng Liu

**Objective:** Downscale lower resolution 500m and 1000m MODIS spectral bands to 250m without additional information to create a spatially consistent 250m MODIS dataset.

**Issue:** MODIS acquires spectral bands at multiple spatial resolutions - 250m, 500m, and 1000m. Retrieving land surface information requires data from multiple spectral bands. **Spectral Indices**, such as Normalized Difference Water Index (NDWI) [1], is a combination of Green (500m) and and NIR (250m) bands of MODIS. Similarly, Normalized Burn Ratio (NBR) [2] incorporates NIR (250m) and SWIR (500m) spectral bands. Therefore, in order to generate spectral indices or work with spectral bands from multiple spatial resolutions we need to resolve the differences.

**Previous Work and Limitations:** To minimize the difference in spatial resolutions, researchers either resample the lower resolution bands to match the resolution of higher resolution bands or the resolution of the lower resolution bands are increased using downscaling techniques. Statistical downscaling methods utilize the relationship between the lower and the higher resolution images to downscale lower resolution bands, for example - ATPRK [3] and EPM [4]. Both ATPRK and EPM assume that the relationship between the lower and the higher resolution bands remain constant, however, this relationship can vary across location, season, and vegetation type [5].

**Solution:** Deep learning methods can be used as a universal function approximator which learns the representations between lower and higher resolution images for downscaling lower resolution MODIS spectral bands. Deep learning methods have the ability to learn from a large number of samples which makes the method more accurate and robust towards outliers. Since there are no higher resolution images of the lower resolution spectral bands available, Wald's protocol [6] can be used to learn the relationships between the low and high-resolution representations of the pixels.

We propose a solution (deep residual encoder-decoder network or **DREDN**) that does not require additional information (unlike ATPRK). DREDN is adapted from the Fastai U-Net model [7]. 

**Model Diagram:**

![MODIS-Downscaling%20a450b882fddf4b2da98541e02396e3d4/UNETDiagram_(3).png](MODIS-Downscaling%20a450b882fddf4b2da98541e02396e3d4/UNETDiagram_(3).png)

High level view of Deep Residual Encoder Decoder Network (DREDN) for Downscaling MODIS spectral bands

**Results:**  We carried out our experiments on MODIS Blue, Green, two shortwave infrared bands (SWIR1 and SWIR2), and two thermal infrared bands (TIR1 and TIR2). Below are the results for Blue, SWIR1, and TIR1.

**SWIR1**

![MODIS-Downscaling%20a450b882fddf4b2da98541e02396e3d4/SWIR1.png](MODIS-Downscaling%20a450b882fddf4b2da98541e02396e3d4/SWIR1.png)

**From Left: Input SWIR band 256x256, by ATRPK, by DREDN, Target**

**TIR1**

![MODIS-Downscaling%20a450b882fddf4b2da98541e02396e3d4/TIR1.png](MODIS-Downscaling%20a450b882fddf4b2da98541e02396e3d4/TIR1.png)

**From Left: Input TIR band 256x256, by ATRPK, by DREDN, Target**

[MODIS Blue (B3)](https://www.notion.so/1560f61919e54b62b5b0c221e6ff6869)

[MODIS SWIR1 (B6)](https://www.notion.so/1d43aae43c004ffa80d267e28ae4b0bc)

[MODIS TIR1 (B31)](https://www.notion.so/efe77d3db3984a4eab0b2fb9f6b0a698)

Validations performed using python sewar library - [https://pypi.org/project/sewar/](https://pypi.org/project/sewar/)

---

References:

[1] McFeeters, Stuart K. "The use of the Normalized Difference Water Index (NDWI) in the delineation of open water features." Internatioal journal of remote sensing 17.7 (1996): 1425-1432.

[2] Keeley, J. E. (2009). Fire intensity, fire severity and burn severity: A brief review and suggested usage. International Journal of Wildland Fire, 18(1), 116–126

[3] Karnieli, Arnon, et al. "Use of NDVI and land surface temperature for drought assessment: Merits and limitations." Journal of climate 23.3 (2010): 618-633.

[4] Wang, Qunming, et al. "Downscaling MODIS images with area-to-point regression kriging." Remote Sensing of Environment 166 (2015): 191-204.

[5] Liu, Desheng, and Xiaolin Zhu. "An enhanced physical method for downscaling thermal infrared radiance." IEEE Geoscience and Remote Sensing Letters 9.4 (2012): 690-694.

[6] Wald, Lucien. "Quality of high resolution synthesised images: Is there a simple criterion?." 2000.

[7] Fastai: U-net model. [https://docs.fast.ai/vision.models.unet.html](https://docs.fast.ai/vision.models.unet.html)
