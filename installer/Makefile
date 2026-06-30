define bin2s_modern
	echo ".set noat" > $(2)
	echo ".set noreorder" >> $(2)
	echo ".section .rodata.\"$(3)\",\"a\",@progbits" >> $(2)
	echo ".align 4" >> $(2)
	echo ".global $(3)" >> $(2)
	echo ".type $(3), @object" >> $(2)
	echo "$(3):" >> $(2)
	echo ".incbin \"$(1)\"" >> $(2)
	echo ".align 4" >> $(2)
	echo "$(3)_end:" >> $(2)
	echo ".global $(3)_end" >> $(2)
	echo ".global size_$(3)" >> $(2)
	echo "size_$(3):" >> $(2)
	echo ".word $(3)_end - $(3)" >> $(2)
endef

EE_BIN = Installer.elf
EE_BIN_PACKED = YoshiBoot_Fortuna_Installer.ELF
EE_BIN_STRIPPED = stripped.elf
EE_OBJS = main.o gs.o pad.o  gs_asm.o ps2_asm.o dma_asm.o
EE_OBJS += YOSHBOOT_ELF.o YOSHCONF_ELF.o opl_elf.o ule_elf.o yoshconf_icn.o yoshconf_sys.o yoshboot_sys.o yoshboot_icn.o exploit_sys.o exploit_bin.o YOSHCONF_CNF.o OpenTuna_SLIMS.o OpenTuna_FAT-170.o OpenTuna_FAT-110-120-150-160.o opl_icn.o opl_sys.o opl_cfg.o ule_cnf.o ule_bg.o opl_dualshock.o pops_usbd.o pops_usbhdfsd.o pops_icn.o pops_sys.o
EE_SRC =   YOSHBOOT_ELF.s YOSHCONF_ELF.s opl_elf.s ule_elf.s yoshconf_icn.s yoshconf_sys.s yoshboot_sys.s yoshboot_icn.s exploit_sys.s exploit_bin.s YOSHCONF_CNF.s OpenTuna_SLIMS.s OpenTuna_FAT-170.s OpenTuna_FAT-110-120-150-160.s opl_icn.s opl_sys.s opl_cfg.s ule_cnf.s ule_bg.s opl_dualshock.s pops_usbd.s pops_usbhdfsd.s pops_icn.s pops_sys.s
EE_LIBS = -ldebug -lcdvd -lpatches -lpad -lmc

ifeq ($(BOOT_FUNTUNA_ON_SUCCESS),1)
	EE_CFLAGS += -DBOOT_FUNTUNA_ON_SUCCESS -DELF_LAUNCHER
endif


all:
	@echo Building YoshiBoot Installer
	$(MAKE) $(EE_BIN_PACKED)

# BOOT
YOSHBOOT_ELF.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/BOOT/BOOT.ELF,YOSHBOOT_ELF.s,YOSHBOOT_ELF)

yoshboot_icn.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/BOOT/yoshboot.icn,yoshboot_icn.s,yoshboot_icn)

yoshboot_sys.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/BOOT/icon.sys,yoshboot_sys.s,yoshboot_sys)
# /BOOT

# EXPLOIT
exploit_bin.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/ENTRYPOINT/exploit.bin,exploit_bin.s,exploit_bin)
	
OpenTuna_SLIMS.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/ENTRYPOINT/slims.bin,OpenTuna_SLIMS.s,opentuna_slims)
	
OpenTuna_FAT-110-120-150-160.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/ENTRYPOINT/fats.bin,OpenTuna_FAT-110-120-150-160.s,opentuna_fats)
	
OpenTuna_FAT-170.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/ENTRYPOINT/170.bin,OpenTuna_FAT-170.s,opentuna_fat170)

exploit_sys.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/ENTRYPOINT/exploit.sys,exploit_sys.s,exploit_sys)
# /EXPLOIT

# OPL
opl_dualshock.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/OPL/conf_game.cfg,opl_dualshock.s,opl_dualshock)

opl_cfg.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/OPL/conf_opl.cfg,opl_cfg.s,opl_cfg)
	
opl_sys.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/OPL/icon.sys,opl_sys.s,opl_sys)

opl_icn.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/OPL/opl.icn,opl_icn.s,opl_icn)
	
opl_elf.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/OPL/OPNPS2LD.ELF,opl_elf.s,opl_elf)

# /OPL

# POPSTARTER
pops_sys.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/POPSTARTER/icon.sys,pops_sys.s,pops_sys)

pops_icn.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/POPSTARTER/pops.icn,pops_icn.s,pops_icn)

pops_usbd.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/POPSTARTER/usbd.irx,pops_usbd.s,pops_usbd)

pops_usbhdfsd.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/POPSTARTER/usbhdfsd.irx,pops_usbhdfsd.s,pops_usbhdfsd)
# /POPSTARTER

# SYS-CONF
yoshconf_sys.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/SYS-CONF/icon.sys,yoshconf_sys.s,yoshconf_sys)

ule_cnf.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/SYS-CONF/LAUNCHELF.CNF,ule_cnf.s,ule_cnf)

YOSHCONF_CNF.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/SYS-CONF/OSDMENU.CNF,YOSHCONF_CNF.s,YOSHCONF_CNF)

ule_elf.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/SYS-CONF/ULE.ELF,ule_elf.s,ule_elf)

ule_bg.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/SYS-CONF/ULEBG.JPG,ule_bg.s,ule_bg)
	
YOSHCONF_ELF.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/SYS-CONF/YOSHCONF.ELF,YOSHCONF_ELF.s,YOSHCONF_ELF)

yoshconf_icn.s:
	@$(call bin2s_modern,INSTALLER_CONTENTS/SYS-CONF/yoshconf.icn,yoshconf_icn.s,yoshconf_icn)
# /SYS-CONF
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
