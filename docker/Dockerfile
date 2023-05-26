# https://github.com/rocker-org/rocker-versioned2

FROM rocker/geospatial:4.2.2

# install shiny server
RUN /rocker_scripts/install_shiny_server.sh  

# OS環境（rockerはdebianベース）に日本語ロケールを追加し切り替え
ENV LANG ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8
RUN sed -i '$d' /etc/locale.gen \
  && echo "ja_JP.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen ja_JP.UTF-8 \
    && /usr/sbin/update-locale LANG=ja_JP.UTF-8 LANGUAGE="ja_JP:ja"
RUN /bin/bash -c "source /etc/default/locale"
RUN ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# 日本語フォントをインストール
RUN apt-get update && apt-get install -y \
  fonts-ipaexfont \
  fonts-noto-cjk

# 疫学のための Rハンドブックの推奨パッケージをimport
# https://epirhandbook.com/jp/packages-suggested.html

RUN install2.r --error --skipinstalled --deps TRUE --ncpu -1\
    tidylog \
    DBI \
    RPostgreSQL \
    odbc \
    pacman \
    here \
    rio \
    openxlsx \
    renv \
    remotes \
    linelist \
    naniar \
    janitor \
    gtsummary \
    rstatix \
    broom \
    lmtest \
    easystats \
    parameters \
    see \
    cowplot \
    patchwork \
    RColorBrewer \
    ggnewscale \
    ggridges \
    DiagrammeR \
    ggrepel \
    plotly \
    gganimate \
    sf \
    tmap \
    OpenStreetMap \
    spdep \
    rmarkdown \
    reportfactory \
    officer \
    flexdashboard \
    shiny \
    knitr \
    flextable \
    DT \
    gt \
    huxtable \
    gsDesign \
    shinydashboard \
    formattable \
    ggplotgui \
    ggraptR \
    MASS \
    rJava \
    pool \
    Rmisc \
    rgdal \
    celestial \
    NipponMap \
    GGally \
    ggmap \
    ggmosaic \
    Hmisc \
    kableExtra \
    mice \
    officer \
    summarytools \
    zipangu \
    coin \
    sessioninfo \
    styler \
    sqldf \
    Matching \
    MatchIt \
    WeightIt \
    epiR \
    cobalt \
    glmnet \
    glmnetUtils \
    rpart \
    partykit \
    pROC \
    caret \
    Amelia \
    tibbletime \
    xts \
    forecast \
    rstan \
    styler \
    survival \
    survminer \
    broom \
    lme4 \
    lmerTest \
    gee \
    geepack \
    emmeans \
    interactions \
    forestplot \
    boot \
    logistf \
    ggsci \
    ggfortify \
    ggbeeswarm \
    ggpubr \
    lubridate \
    haven \
    esquisse \
    tableone \
    RMySQL \
    jsonlite \
    checkpoint \
    emmeans \
    curl \
    doParallel \
    reshape2 \
    qlcMatrix \
    proxy \
    moments \
    greybox \
    muhaz \
    rpart.plot \
    ranger \
    xgboost \
    tm \
    SnowballC \
    text2vec \
    kernlab \
    rpivotTable \
    DataExplorer \
    skimr \
    XLConnect \
    mlr \
    terra \
    spData \
    mapview \
    osrm \
    movecost \
    miniCRAN \
    rjson

# GitHubからのインストール
RUN installGithub.r \
  uribo/jpmesh \
  uribo/jpndistrict \
  mlr-org/shinyMlr 

# パッケージ追加 20230517
RUN install2.r --error --skipinstalled --deps TRUE --ncpu -1\
    gghighlight \
    ggThemeAssist \
    targets \
    revealjs \
    docxtractr \
    cronR \
    export

# 参考:Rstudio serverの細かい設定をdockerfileから自動化する
# https://qiita.com/taiyodayo/items/49b90e785b1c6ce828b8

# 設定ファイルのcopy
COPY --chown=rstudio:rstudio rstudio-prefs_mysettings.json \
    /home/rstudio/.config/rstudio/rstudio-prefs.json

# Rプロファイルをコピー - RStudio起動時に実行したいRスクリプトをこのファイルに書くことが出来る
# RStudioのみ再起動した場合も読み込まれます
COPY --chown=rstudio:rstudio dotRprofile /home/rstudio/.Rprofile

RUN sudo chown -R rstudio:rstudio /home/rstudio \
    # 設定ファイルの権限変更
    && chmod 755 /home/rstudio/.config/rstudio/rstudio-prefs.json \
    # インストール時にダウンロードした一時ファイルの削除
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds
