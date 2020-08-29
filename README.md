# installation
Installation software for Linux


# 1. General installation
Downland .tar archive and then make next commands in terminal:
```
tar -zxvf example.tar.gz
cd example
./bootstrap
make
sudo make install
```


# 2. Install Geant4 10.6 and prerequisites
[http://geant4-userdoc.web.cern.ch/geant4-userdoc/UsersGuides/InstallationGuide/]

1) Update programs
```
sudo apt-get update
sudo apt-get upgrade
```

2) Install openssl and libssl-dev
```
sudo apt-get --fix-missing install git dpkg-dev cmake g++ gcc binutils libx11-dev libxpm-dev libxft-dev libxext-dev gfortran libssl-dev libpcre3-dev xlibmesa-glu-dev libglew1.5-dev libftgl-dev libmysqlclient-dev libfftw3-dev libcfitsio-dev graphviz-dev libavahi-compat-libdnssd-dev libldap2-dev python-dev libxml2-dev libkrb5-dev libgsl0-dev libqt4-dev doxygen doxygen-gui ipython ipython-qtconsole build-essential python-pip
```
3) Install latest cmake binaries from [https://cmake.org/download/]
```
wget https://github.com/Kitware/CMake/releases/download/v3.18.2/cmake-3.18.2.tar.gz
tar -zxvf cmake-3.18.2.tar.gz
cd cmake-3.18.2
./bootstrap
make
sudo make install
cmake --version
```
* Add path to cmake binaries in the PATH variable `export PATH=$HOME/soft/cmake-3.18.2/bin:$PATH`
4) Install CLHEP [http://proj-clhep.web.cern.ch/proj-clhep/INSTALLATION/clhep-2.0.html]
```
mkdir clhep-build clhep-install
cd clhep-build
cmake -DCMAKE_INSTALL_PREFIX=~/software/clhep-install ~/software/clhep-2.4.1.3/CLHEP/
cmake --build . --config RelWithDebInfo
ctest
cmake --build . --target install
```
5) Install Xerces-C++ [http://xerces.apache.org/xerces-c/download.cgi]
```
mkdir xerces-build xerces-install
cd xerces-build
cmake -DCMAKE_INSTALL_PREFIX=~/software/xerces-install ~/software/xerces-c-3.2.3
make
make test
make install
```
6) Upgrade video drivers [http://geant4-userdoc.web.cern.ch/geant4-userdoc/UsersGuides/InstallationGuide/html/gettingstarted.html]
7) Download geant4 sources from: [https://geant4.web.cern.ch/support/download]
6) mkdir $HOME/soft/geant4.10.06-build
7) cd $HOME/soft/geant4.10.06-build
8) cmake -DGEANT4_USE_OPENGL_X11=ON -DGEANT4_USE_XM=ON -DGEANT4_USE_QT=ON -DGEANT4_INSTALL_DATA=ON -DCMAKE_INSTALL_PREFIX=$HOME/soft/geant4.10.06-install $HOME/soft/ge$
9) make -j6
10) initialize geant4 environment (also add it in your aspirantura.sh)
source $HOME/soft/geant4.10.06-install/bin/geant4.sh

# 3. Install PYTHIA
1) cd $HOME/soft
2) download latest pythia from http://home.thep.lu.se/~torbjorn/Pythia.html
3) tar -zxvf pythia8243.tgz
4) cd pythia8243
5) ./configure --enable-shared
6) make
7) add this line in aspirantura.sh (loaded in .bashrc):
export PYTHIA8=$HOME/soft/pythia8243
export PYTHIA8DATA=$PYTHIA8/share/Pythia8/xmldoc
LD_LIBRARY_PATH=$PYTHIA8/lib:$LD_LIBRARY_PATH

# 4. Install ROOT
1) git clone http://github.com/root-project/root.git
2) cd root
3) git checkout -b v6-18-04 v6-18-04
4) cd ..
5) mkdir root_build
6) cd root_build
7) cmake -DCMAKE_INSTALL_PREFIX=$HOME/aspirantura/root_install -Dpythia8=ON -DPYTHIA8_DIR=$PYTHIA8 -DPYTHIA8_INCLUDE_DIR=$PYTHIA8/include -DPYTHIA8_LIBRARY=$PYTHIA8/li$
8) make -j6
9) make install

# 5. Install GARFIELD++ (requires root)
More details: https://garfieldpp.web.cern.ch/garfieldpp/getting-started/
1) export GARFIELD_HOME=$HOME/soft/garfield
2) git clone https://gitlab.cern.ch/garfield/garfieldpp.git $GARFIELD_HOME
3) cd $GARFIELD_HOME
4) mkdir build
5) cd build
6) cmake -DCMAKE_INSTALL_PREFIX=$HOME/soft/garfield_install -DWITH_EXAMPLES=OFF $GARFIELD_HOME
7) make install
8) add these lines in aspirantura.sh (loaded in .bashrc):
export GARFIELD_HOME=$HOME/soft/garfield_install
export LD_LIBRARY_PATH=$GARFIELD_HOME/lib:$LD_LIBRARY_PATH
