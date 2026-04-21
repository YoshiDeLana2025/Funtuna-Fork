EE_BIN = Installer.elf
EE_BIN_PACKED = YoshiBoot_Fortuna_Installer.ELF
EE_BIN_STRIPPED = stripped.elf
EE_OBJS = main.o gs.o pad.o  gs_asm.o ps2_asm.o dma_asm.o
EE_OBJS += YOSHBOOT_ELF.o opl_elf.o ule_elf.o yoshconf_icn.o yoshconf_sys.o yoshboot_sys.o yoshboot_icn.o exploit_sys.o exploit_bin.o YOSHCONF_CNF.o OpenTuna_SLIMS.o OpenTuna_FAT-170.o OpenTuna_FAT-110-120-150-160.o opl_icn.o opl_sys.o pops_usbd.o pops_usbhdfsd.o pops_icn.o pops_sys.o
EE_SRC =   YOSHBOOT_ELF.s opl_elf.s ule_elf.s yoshconf_icn.s yoshconf_sys.s yoshboot_sys.s yoshboot_icn.s exploit_sys.s exploit_bin.s YOSHCONF_CNF.s OpenTuna_SLIMS.s OpenTuna_FAT-170.s OpenTuna_FAT-110-120-150-160.s opl_icn.s opl_sys.s pops_usbd.s pops_usbhdfsd.s pops_icn.s pops_sys.s
EE_LIBS = -ldebug -lcdvd -lpatches -lpad -lmc

ifeq ($(BOOT_FUNTUNA_ON_SUCCESS),1)
	EE_CFLAGS += -DBOOT_FUNTUNA_ON_SUCCESS -DELF_LAUNCHER
endif


all:
	@echo Building YoshiBoot Installer
	$(MAKE) $(EE_BIN_PACKED)

# BOOT
YOSHBOOT_ELF.s:
	@bin2s INSTALLER_CONTENTS/BOOT/BOOT.ELF YOSHBOOT_ELF.s YOSHBOOT_ELF

yoshboot_icn.s:
	@bin2s INSTALLER_CONTENTS/BOOT/yoshboot.icn yoshboot_icn.s yoshboot_icn

yoshboot_sys.s:
	@bin2s INSTALLER_CONTENTS/BOOT/icon.sys yoshboot_sys.s yoshboot_sys	
# /BOOT

# SYS-CONF

YOSHCONF_CNF.s:
	@bin2s INSTALLER_CONTENTS/SYS-CONF/OSDMENU.CNF YOSHCONF_CNF.s YOSHCONF_CNF

yoshconf_icn.s:
	@bin2s INSTALLER_CONTENTS/SYS-CONF/yoshconf.icn yoshconf_icn.s yoshconf_icn

yoshconf_sys.s:
	@bin2s INSTALLER_CONTENTS/SYS-CONF/icon.sys yoshconf_sys.s yoshconf_sys

ule_elf.s:
	@bin2s INSTALLER_CONTENTS/SYS-CONF/ULE.ELF ule_elf.s ule_elf

# /SYS-CONF

# OPL
opl_elf.s:
	@bin2s INSTALLER_CONTENTS/OPL/OPNPS2LD.ELF opl_elf.s opl_elf

opl_icn.s:
	@bin2s INSTALLER_CONTENTS/OPL/opl.icn opl_icn.s opl_icn
	
opl_sys.s:
	@bin2s INSTALLER_CONTENTS/OPL/icon.sys opl_sys.s opl_sys
		
# /OPL

# POPSTARTER

pops_icn.s:
	@bin2s INSTALLER_CONTENTS/POPSTARTER/pops.icn pops_icn.s pops_icn

pops_sys.s:
	@bin2s INSTALLER_CONTENTS/POPSTARTER/icon.sys pops_sys.s pops_sys

pops_usbd.s:
	@bin2s INSTALLER_CONTENTS/POPSTARTER/usbd.irx pops_usbd.s pops_usbd

pops_usbhdfsd.s:
	@bin2s INSTALLER_CONTENTS/POPSTARTER/usbhdfsd.irx pops_usbhdfsd.s pops_usbhdfsd

# /POPSTARTER


# EXPLOIT
exploit_bin.s:
	@bin2s INSTALLER_CONTENTS/ENTRYPOINT/exploit.bin exploit_bin.s exploit_bin
	
OpenTuna_SLIMS.s:
	@bin2s INSTALLER_CONTENTS/ENTRYPOINT/slims.bin OpenTuna_SLIMS.s opentuna_slims
	
OpenTuna_FAT-110-120-150-160.s:
	@bin2s INSTALLER_CONTENTS/ENTRYPOINT/fats.bin OpenTuna_FAT-110-120-150-160.s opentuna_fats
	
OpenTuna_FAT-170.s:
	@bin2s INSTALLER_CONTENTS/ENTRYPOINT/170.bin OpenTuna_FAT-170.s opentuna_fat170


exploit_sys.s:
	@bin2s INSTALLER_CONTENTS/ENTRYPOINT/exploit.sys exploit_sys.s exploit_sys
# /EXPLOIT
clean:
	@echo cleaning...
	@echo ...objs and $(EE_BIN_PACKED) $(EE_BIN_STRIPPED) $(EE_BIN)
	@rm -fr *.o $(EE_BIN_PACKED) $(EE_BIN_STRIPPED) $(EE_BIN)
	@echo ...embedded resources
	@rm -fr FMCB_ELF.* FMCB_CNF.* CFG_ELF.* opl_elf.* ule_elf.* apps_icn.* apps_sys.* poweroff_elf.* FUNTUNA_USBHDFSD.* FUNTUNA_USBD.* ule_cnf.* boot_sys.* boot_icn.* OpenTuna_SLIMS.* OpenTuna_FAT-170.* OpenTuna_FAT-110-120-150-160.* opl_icn.* opl_sys.* opl_cfg.* opl_cfg1.* opl_dualshock.*

clean-bin:
	@rm $(EE_BIN_PACKED) 
	@rm $(EE_BIN_STRIPPED) 
	@rm $(EE_BIN)

$(EE_BIN_STRIPPED): $(EE_BIN)
	$(EE_STRIP) -o $@ $<

$(EE_BIN_PACKED): $(EE_BIN_STRIPPED)
	ps2-packer $< $@ > /dev/null

include $(PS2SDK)/samples/Makefile.pref
include $(PS2SDK)/samples/Makefile.eeglobal
