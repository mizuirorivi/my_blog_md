# .rela.dyn
###### tags: `pwn` `readelf` `linux` `rela.dyn` `got` `plt`

.rela.dyn is a section in the ELF format that holds RELA type relocation information for all sections of a shared library except the PLT The addend is specified in the relocation itself. It is one of several relocation tables in the ELF format.

## Ref
- https://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-S390/LSB-Core-S390/sections.html