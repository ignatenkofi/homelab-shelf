## FlashFig is done, but a configuration is not applied 

If all procedures went successfully, but RouterOS configuration from .rsc file is not applied, add startup delay to *.rsc configuration file. The reason might be, that the configuration script is executed before all interfaces boots up.
