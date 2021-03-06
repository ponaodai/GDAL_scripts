**Description:**
    IAU2000_v2.wkt is a tabular Well Known Text (WKT) representation of the
    IAU2000 coded coordinate reference systems (CRS) for planetary bodies
    for use by Open GeospatialConsortium (OGC) web services (e.g. WMS,
    WCS, ect.). This is meant to be used like the EPSG Earth CRS codes.
    IAU2009_v2.wkt references the IAU codes as defined in the 2009 paper (below).

    The OGC paper, docs\OpenGIS_Project_Document_06-119_Hare.doc, explains
    the proposal for using this WKT projection table.

**Source directory:**
    create_IAU2000_wkt_v2.py is a Python script creates a IAU2000 WKT
    for Open Geospatial Consortium WMS services from the 
    naifcodes_radii_m_wAsteroids_IAU2000.csv driver file.  
    It will create a IAU2000 coded system (similar to EPSG codes) for
    planetary bodies.
    
iau2wkt.c is a converted C program to do the same as above (http://github.com/YannChemin/iau2wkt).
This was converted by Yann Chamin for potential addition to GDAL

 **Feb 2016:**
---- update to report IAU Mean from reports, 
---- Asteroids and IAU reported Comets,
---- and two new projections (Mollweide and Robinson)
 
**March 2016:**
---- added IAU authority, cleaned code (pep8), added refs and updated albers to stndPar_1,2,center_lat=60,20,40

**July 2016:**
---- changed "Decimal_Degree" to just "Degree"

**July 2017:**
---- updated to support -1 (NoData) in naifcodes_radii_m_wAsteroids_IAUxxxx.csv
---- updated to Python 3 (not much changed since such a simple script)

source usage: create_IAU2000_wkt_v2.py naifcodes_radii_m_wAsteroids_IAU2000.csv [output.wtk]

**INPUT:** (naifcodes_radii_m_wAsteroids_IAU2000.csv or naifcodes_radii_m_wAsteroids_IAU2009.csv)
**Example file format:**
Naif_id,Body,IAU2000_Mean,IAU2000_Semimajor,IAU2000_Axisb,IAU2000_Semiminor
199,Mercury,2439700.00,2439700.00,2439700.00,2439700.00
299,Venus,6051800.00,6051800.00,6051800.00,6051800.00
399,Earth,6371000.00,6378140.00,6378140.00,6356750.00
301,Moon,1737400.00,1737400.00,1737400.00,1737400.00
499,Mars,3389500.00,3396190.00,3396190.00,3376200.00
401,Phobos,11100.00,13400.00,11200.00,9200.00
402,Deimos,6200.00,7500.00,6100.00,5200.00


**OUTPUT Example:**
GEOGCS["Mars 2000",DATUM["D_Mars_2000",SPHEROID["Mars_2000_IAU_IAG",3396190.0,169.8944472236118]],PRIMEM["Reference_Meridian",0],UNIT["Degree",0.0174532925199433],AUTHORITY["IAU2000","49900"]]

**Direct use from github:**
Using gdal tools (w/ curl installed for web access) you can use these projections directly to assign projections to images or vectors or to use for re-projection. For example:

$ gdalwarp -t_srs "http://raw.githubusercontent.com/USGS-Astrogeology/GDAL_scripts/master/OGC_IAU2000_WKT_v2/IAU2000_prjs/Moon%202000.prj" my_moonMap.img out_moonMap_inDegrees.tif

Note you need to point to the "raw" address from github. Also you can substitue "https" to "http" . To test you can also run gdalsrsinfo (remember gdal must be built with curl):

$ gdalsrsinfo http://raw.githubusercontent.com/USGS-Astrogeology/GDAL_scripts/master/OGC_IAU2000_WKT_v2/IAU2000_prjs/Moon%202000.prj

contact:
Trent Hare
Astrogeology, U.S.G.S
thare@usgs.gov

The sources for the constants listed in this file for 2000 and 2009 are:

        [1]   Seidelmann, P.K., Abalakin, V.K., Bursa, M., Davies, M.E.,
              Bergh, C. de, Lieske, J.H., Oberst, J., Simon, J.L.,
              Standish, E.M., Stooke, P., and Thomas, P.C. (2002).
              "Report of the IAU/IAG Working Group on Cartographic
              Coordinates and Rotational Elements of the Planets and
              Satellites: 2000," Celestial Mechanics and Dynamical
              Astronomy, v.82, Issue 1, pp. 83-111.

        [2]   Archinal, B. A., M. F. A¦Hearn, E. Bowell, A. Conrad,
               G. J. Consolmagno, R. Courtin, T. Fukushima, D. Hestroffer,
               J. L. Hilton, G. A. Krasinsky, G. Neumann, J. Oberst,
               P. K. Seidelmann, P. Stooke, D. J. Tholen, P. C. Thomas,
               I. P. Williams (2011), "Report of the IAU/IAG Working Group
              on Cartographic Coordinates and Rotational Elements of the
              Planets and Satellites: 2009," Celestial Mechanics and Dynamical
              Astronomy, v.109, Issue 2, pp. 101-135.
