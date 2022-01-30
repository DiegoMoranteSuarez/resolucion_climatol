Ejercicios Paquete Climatol
================
Diego Morante
30/1/2022

``` r
library(climatol)
```

    ## Loading required package: maps

    ## Loading required package: mapdata

# Nivel 1

1.  Generar un diagrama de Walter y Lieth con la data de datcli, este
    debe llevar de título “Estación Campo de Marte”, a una altitud de 80
    msnm durante el año 2017, con los meses simbolizados por números.
    Las temperaturas deberán visualizarse de color verde; las
    precipitaciones, en naranja; los meses de congelación segura, en
    azul y los de congelación probable, en celeste. No trazar una línea
    suplementaria de precipitación.

``` r
data("datcli")
diagwl(datcli,"Estación Campo de Marte", 80, "2017", mlab = "xd", pcol = "orange", tcol = "blue", pfcol = "light blue", sfcol = "blue", p3line = F)
```

![](Resolución-Climatol_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

2.  Recrea minuciosamente el siguiente diagrama de la rosa de los
    vientos (pista: col=rainbow(8)).

``` r
data("windfr")
rosavent(windfr, fnum=6, fint=2, flab=1, ang= 3*pi/8, col=rainbow(8), uni = "km/s")
```

![](Resolución-Climatol_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

# Nivel II

3.  Convertir la data diaria de tmax en una data de medias mensuales.
    Posteriormente, homogeneizar dichos datos mensuales con una
    normalización por estandarización y gráficos de medias anuales y
    correcciones aplicadas en el análisis exploratorio de datos
    (utilizar dos decimales).

``` r
setwd("C:/Users/diego/Documents/R-DiegoMoranteSuarez-UNMSM/climatol")
data(tmax)
# Exportación de archivos
write.table(dat, "tmax_2001-2003.dat", row.names = F, col.names = F)
write.table(est.c, "tmax_2001-2003.est", row.names = F, col.names = F)
# Conversion de (.dat) diario a media mensual
dd2m("tmax", 2001, 2003, ndec = 2, valm = 2)
```

    ##   1  2  3
    ## 
    ## Monthly mean values saved to file tmax-m_2001-2003.dat 
    ##   (Months with more than 10 missing original daily data
    ##   have also been set to missing)

``` r
tmax_m <- read.table("tmax-m_2001-2003.dat", header = F)
# Homogenización
homogen("tmax", 2001, 2003, nm = 0, std = 3, ndec = 2, gp = 3, expl = T)
```

    ## 
    ## HOMOGEN() APPLICATION OUTPUT  (From R's contributed package 'climatol' 3.1.1)
    ## 
    ## =========== Homogenization of tmax, 2001-2003. (Sun Jan 30 04:37:59 2022)
    ## 
    ## Parameters: varcli=tmax anyi=2001 anyf=2003 suf=NA nm=0 nref=10,10,4 std=3 swa=NA ndec=2 dz.max=5 dz.min=-5 wd=0,0,100 snht1=0 snht2=0 tol=0.02 maxdif=0.005 mxdif=0.005 maxite=999 force=FALSE wz=0.001 trf=0 mndat=NA gp=3 ini=NA na.strings=NA vmin=NA vmax=NA nclust=100 cutlev=NA grdcol=#666666 mapcol=#666666 hires=TRUE expl=TRUE metad=FALSE sufbrk=m tinc=NA tz=UTC cex=1.2 verb=TRUE
    ## 
    ## Data matrix: 1095 data x 3 stations

    ## Computing inter-station distances:  1  2
    ## 
    ## 
    ## ========== STAGE 3 (Final computation of all missing data) ==========
    ## 
    ## Computing inter-station weights... (done)

    ## Computation of missing data with outlier removal
    ## (Suggested data replacements are provisional)
    ## 
    ## The following lines will have one of these formats:
    ##   Station(rank) Date: Observed -> Suggested (Anomaly, in std. devs.)
    ##   Iteration Max.data.difference (Station_code)
    ## 2 -0.1884 (S01)
    ## 3 -0.0407 (S01)
    ## 4 -0.0088 (S01)
    ## 5 -0.0019 (S01)
    ## 
    ## Last series readjustment (please, be patient...)

    ## 
    ## ======== End of the missing data filling process, after 0.75 secs 
    ## 
    ## ----------- Final computations:
    ## 
    ## ACmx: Station maximum absolute autocorrelations of anomalies
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##  0.4900  0.5050  0.5200  0.5167  0.5300  0.5400 
    ## 
    ## SNHT: Standard normal homogeneity test (on anomaly series)
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   16.30   26.95   37.60   42.57   55.70   73.80 
    ## 
    ## RMSE: Root mean squared error of the estimated data
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   3.544   3.642   3.739   3.699   3.776   3.814 
    ## 
    ## POD: Percentage of original data
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   81.00   84.50   88.00   87.33   90.50   93.00 
    ## 
    ##   ACmx SNHT RMSE POD Code Name     
    ## 1 0.54 73.8 3.5  81  S01  La Vall  
    ## 2 0.52 37.6 3.7  88  S02  Lucent   
    ## 3 0.49 16.3 3.8  93  S03  Sunflower

    ## 
    ## ----------- Generated output files: -------------------------
    ## 
    ## tmax_2001-2003.txt :  This text output 
    ## tmax_2001-2003_out.csv :  List of corrected outliers 
    ## tmax_2001-2003_brk.csv :  List of corrected breaks 
    ## tmax_2001-2003.pdf :  Diagnostic graphics 
    ## tmax_2001-2003.rda :  Homogenization results. Postprocess with (examples):
    ##    dahstat('tmax',2001,2003) #get averages in file tmax_2001-2003-me.csv 
    ##    dahstat('tmax',2001,2003,stat='tnd') #get OLS trends and their p-values 
    ##    dahgrid('tmax',2001,2003,grid=YOURGRID) #get homogenized grids 
    ##    ... (See other options in the package documentation)

4.  Recortar la data mensual de Ptest desde 1965 hasta 2005.
    Homogeneizar dicha data mediante clústers o áreas rectangulares, con
    un ancho de superposición de 0, mediante una estandarización y con
    gráficos de totales anuales en el análisis exploratorio de datos.
    Mostrar las medias de las series homogeneizadas en un archivo Excel
    que, además, mencione los totales anuales y los datos de la latitud,
    longitud y nombre de cada estación (utilizar dos decimales).
