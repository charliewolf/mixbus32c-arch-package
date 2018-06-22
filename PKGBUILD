# Maintainer: Alexander Mcmillan <linuxguy93@gmail.com> 
# Software Vendor: Harrison Consoles <mixbus@harrisonconsoles.com>

pkgname=mixbus32c
pkgver=4.3.19
pkgrel=3
pkgdesc="Harrison Mixbus - Digital Audio Workstation"
arch=('x86_64')
url="http://harrisonconsoles.com/site/mixbus32c.html"
license=('EULA, GPLv2')
depends=('xorg-server')
provides=('mixbus4' 'mixbus32c')
conflicts=('mixbus4')
source=("http://www.harrisonconsoles.com/mixbus/mb4/releases/Mixbus32C-4.3.19-x86_64-gcc5.tar"
	"mixbus32c.png")
sha256sums=('a9a9172ef378977314b06e68b0ca16062292f965a7e614cc9e73fc515fa03629' 
            'bcffc2ef528a43e1b168dfa7ec35bc2210f54c59e60bce17cb56994975a2513e')

build() {
## Change to source directory
cd $srcdir

## Setup mixbus for installation
# Unpack intallation files
echo "Preparing Installation..."

echo "Unpacking Installer..."
tar -xf Mixbus32C-$pkgver-64bit-gcc5.tar
./Mixbus32C-$pkgver-x86_64-gcc5.run --tar xf 
find . ! -name "Mixbus32C_x86_64-$pkgver.tar" -type f -exec rm -f {} +
tar -xf Mixbus32C_x86_64-$pkgver.tar

}

package() {
## Change into package directory
cd $pkgdir

## Create package directories
echo "Creating Directories..."
mkdir -p opt/$pkgname
mkdir -p usr/local/bin
mkdir -p usr/local/lib
mkdir -p usr/share/applications

## Copy installation directory to package directory
echo "Getting Ready To Package..."
cp -r $srcdir/Mixbus32C_x86_64-$pkgver/* opt/$pkgname
cp $srcdir/mixbus32c.png opt/$pkgname/share

## Create links to excuteables
ln -sr ./opt/$pkgname/bin/mixbus32c ./usr/local/bin/mixbus32c
ln -sr ./opt/$pkgname/lib/LV2 ./usr/local/lib/lv2

## Create a .desktop file
echo "Creating A Desktop Entry..."
echo -e "[Desktop Entry]\nEncoding=UTF-8\nVersion=1.0\nType=Application\nTerminal=false\nExec=/opt/$pkgname/bin/mixbus32c4\nName=Mixbus32C\nIcon=/opt/$pkgname/share/mixbus32c.png\nComment=Digital Audio Workstation\nCategories=AudioVideo;AudioEditing;Audio;Recorder;" > usr/share/applications/mixbus32c.desktop

# Mark as excuteable
chmod 755 usr/share/applications/mixbus32c.desktop

# Time will tell if this harms anything but this allows me to use plugins that link to gtk/glib/etc
for lib in libfreetype.so.6  libgio-2.0.so.0  libglib-2.0.so.0  libgobject-2.0.so.0  libharfbuzz.so.0; do
    rm ./opt/$pkgname/lib/$lib;
done

## Remove package and source directories
echo "Cleaning Up Installation..." 
rm -r $srcdir

## Package has built successfully message
echo "Package Built Successfully!!"
}
