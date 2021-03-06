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
sudo apt-get install openssl
sudo apt-get install libssl-dev
wget https://github.com/Kitware/CMake/releases/download/v3.18.2/cmake-3.18.2.tar.gz
tar -zxvf cmake-3.18.2.tar.gz
cd cmake-3.18.2
./bootstrap
make
sudo make install
export PATH=$HOME/soft/cmake-3.18.2/bin:$PATH ## Add path to cmake binaries in the PATH variable
cmake --version
```
4) Install CLHEP [http://proj-clhep.web.cern.ch/proj-clhep/INSTALLATION/clhep-2.0.html]
Downland from [http://proj-clhep.web.cern.ch/proj-clhep/clhep23.html]
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
```
sudo apt install qt5-default
sudo apt-get install mesa-common-dev
sudo apt install x11-utils
sudo apt-get install libx11-dev
sudo apt install libxmu-dev
sudo apt install libmotif-dev
```
For CenOS 7:
```
sudo yum install qt5-qtbase-devel
sudo yum install mesa-libGLU
sudo yum install xorg-x11-server-Xorg xorg-x11-xauth xorg-x11-apps
sudo yum install libX11
sudo yum install libXmu
sudo yum install motif-devel
sudo yum install expat-devel
sudo yum install libXmu-devel
```
7) Download geant4 sources from: [https://geant4.web.cern.ch/support/download] and then
```
mkdir geant4-build geant4-install
cd geant4-build
cmake -DGEANT4_USE_OPENGL_X11=ON -DGEANT4_USE_XM=ON -DGEANT4_USE_QT=ON -DGEANT4_INSTALL_DATA=ON -DCMAKE_INSTALL_PREFIX=~/software/geant4-install ~/software/geant4.10.06.p02
make
make test
make install
source $HOME/software/geant4-install/bin/geant4.sh
```
8) Compilate program for Geant4:
```
mkdir built
cd built
cmake ..
make
./progName
/run/beamOn 100000000
```

# 3. Install PYTHIA
* PYTHIA install before ROOT. Download latest pythia from [http://home.thep.lu.se/~torbjorn/Pythia.html]
```
tar -zxvf pythia8302.tgz
cd pythia8302
./configure --enable-shared
make
```
* Add this lines in `.bashrc`:
```
export PYTHIA8=$HOME/software/pythia8302
export PYTHIA8DATA=$PYTHIA8/share/Pythia8/xmldoc
export LD_LIBRARY_PATH=$PYTHIA8/lib:$LD_LIBRARY_PATH
```

# 4. Install ROOT
* Check dependencies [https://root.cern/install/dependencies/]  
```
sudo yum install git cmake3 gcc-c++ gcc binutils \
libX11-devel libXpm-devel libXft-devel libXext-devel openssl-devel

sudo yum install gcc-gfortran pcre-devel \
mesa-libGL-devel mesa-libGLU-devel glew-devel ftgl-devel mysql-devel \
fftw-devel cfitsio-devel graphviz-devel \
avahi-compat-libdns_sd-devel openldap-devel python-devel \
libxml2-devel gsl-devel
```
* Downland sourse from the link [https://root.cern/install/all_releases/]
* Installation guide [https://root.cern/install/]
```
mkdir root-install root-build
cd root-build
cmake -DCMAKE_INSTALL_PREFIX=$HOME/software/root-install ~/software/root-6.22.02 -Dpythia8=ON -DPYTHIA8_DIR=$PYTHIA8 -DPYTHIA8_INCLUDE_DIR=$PYTHIA8/include -DPYTHIA8_LIBRARY=$PYTHIA8/lib/libpythia8.so ../root -Dminuit2=ON -Dmathmore=ON -Dcxx14=ON
make
make install
cd bin
source thisroot.sh
```
* Add source to the `/.bashrc`:
```
export ROOTSYS=/home/lkst/software/root-build
export PATH=$ROOTSYS/bin:$PATH
export LD_LIBRARY_PATH=$ROOTSYS/lib/:$LD_LIBRARY_PATH
```

# 5. Install GARFIELD++ (requires root)
* Installation instructions and source files in [https://garfieldpp.web.cern.ch/garfieldpp/getting-started/]
```
export GARFIELD_HOME=$HOME/software/garfield
git clone https://gitlab.cern.ch/garfield/garfieldpp.git $GARFIELD_HOME
cd $GARFIELD_HOME
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=$HOME/software/garfield/install -DWITH_EXAMPLES=OFF $GARFIELD_HOME
make
make install
```
* Add these lines in .bashrc:
```
export GARFIELD_HOME=$HOME/software/garfield
export LD_LIBRARY_PATH=$GARFIELD_HOME/install/lib/:$LD_LIBRARY_PATH
export CMAKE_PREFIX_PATH=$GARFIELD_HOME/install:${CMAKE_PREFIX_PATH}
export HEED_DATABASE=$GARFIELD_HOME/Heed/heed++/database
source $GARFIELD_HOME/build/setup.sh
```
* Make project:
```
mkdir build 
cd build
cmake ..
make
./example
```
