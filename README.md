# myrocker-geo-shiny

rstudio server and shiny server and many package

base : rocker/geospatial:4.2.2
add : shiny server

## docker run sample

docker run --rm -d -p 28787:8787 -p 23838:3838 -e PASSWORD=rs -e ROOT=TRUE -v $PWD/srv/:/home/rstudio/srv/ -v $PWD/srv/shinyapps/:/srv/shiny-server/ -v $PWD/srv/shinylog/:/var/log/shiny-server/ --name nujabec/myrocker-geo-shiny:0.6 myrocker-geo-shiny

## docker-compose sample

docker-compose build 

docker-compose up -d

