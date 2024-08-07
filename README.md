# linux_buisness_card
===============================


**Все изменения от корня git (businesscard-linux)**  
файл ./config.in  
закоментировать строку  
#source "$BR2_EXTERNAL_BUSINESSCARD_PATH/package/fortune-mod/Config.in"  
в файле ./configs/thirtythreeforty_businesscard_defconfig  
Строку BR2_LINUX_KERNEL_CUSTOM_REPO_URL="git://github.com/thirtythreeforty/linux.git"    
заменить на  
BR2_LINUX_KERNEL_CUSTOM_REPO_URL=" https ://github.com/thirtythreeforty/linux.git"  
строку BR2_TARGET_UBOOT_CUSTOM_REPO_URL="git://github.com/thirtythreeforty/u-boot.git"  
заменить на  
BR2_TARGET_UBOOT_CUSTOM_REPO_URL=" https ://github.com/thirtythreeforty/uboot.git"  
строки BR2_PACKAGE_FORTUNE_MOD=y и   
BR2_PACKAGE_FORTUNE_MOD_COOKIES="computers;humorists;linuxcookie;literature;pratchett;startrek;wisdom"   
закоменитровать (#)  
в папке ./package/businesscard-flashdrive/files/ удалить ВСЕ КРОМЕ genimage.cfg  
скопировать в папку /package/businesscard-flashdrive/files/ присланные мной файлы   
(презентации)  
файл genimage.cfg привести к виду (ОСОБОЕ ВНИМАНИЕ К ЗАПЯТЫМ):  
image flashdrive.vfat {  
vfat {  
files = {  
"autorun.inf",  
"carwash.ico",  
"EPI_Carwash_Pres.pdf",  
"EPI_Carwash_Tech_Pres.pdf",  
"links.pdf"  
}  
}  
size = 2816K  
}  
image flashdrive.img {  
hdimage {}  
partition businesscard {  
partition-type = 0xc  
image = "flashdrive.vfat"  
}  
}  
в консоли системы на которой компилируется система выполнить:  
cd buildroot  
eval $(perl -Mlocal::lib=--deactivate-all)  
а дальше как по книжке  
make clean  
make BR2_EXTERNAL=$PWD/../ thirtythreeforty_businesscard_defconfig  
и вот так  
FORCE_UNSAFE_CONFIGURE=1  
make  
вставить плату и выполнить lsusb  
должны быть в ответе строка   
Omni devise тратата in FEL mode (или in flash mode)  
смело выполняем  
output/host/bin/sunxi-fel -p spiflash-write 0 output/images/flash.bin  
