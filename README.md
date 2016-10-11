# atlas_mapproxy

This project contains all the mapproxy files for the Datapunt Map project.

To Run this:

    docker-compose build
    
    docker-compose run topo-kbk

seed.yaml - Caching configuratie
mapproxy.yaml - Mapproxy server config

---------------------

Luchtfoto tegels
----------------

Creating a new Lufo year of tiles and service follow these steps:

1. Copy the aerial pictures (tif) to localhost
2. Run mapserver/lufopyramids.sh (see comments in file)
3. Start mapserver docker
4. Run mapproxy docker:

    docker-compose run topo-kbk


5. Copy generated tiles from /mnt/tiles/lufo_rd_cache_EPSG28992/ to: /mnt/tiles/lufo<YEAR>_rd_cache_EPSG28992/
6. Upload the tiles to the objectstore:


    lftp -e 'mirror --ignore-time --no-perms --no-umask --only-missing -R -p -v -P 10 /mnt/tiles/lufo<YEAR>_rd_cache_EPSG28992/ /tiles/lufo<YEAR>_rd_cache_EPSG28992/' ftp.objectstore.eu    
    
7. Upload pyramid directory to objectstore
