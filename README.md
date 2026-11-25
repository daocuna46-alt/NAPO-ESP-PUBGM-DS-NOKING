# NAPO-ESP-PUBGM-DS-NOKING

NAPO ESP Pubg DS (login bypass patch) — unsigned IPA.

V3 changes:
- login gate -> hack screen (SwitchToLoginScreen @ 0x10008954c -> b 0x100088768)
- zeroed __qbl_guard, __qbl_auth, __qbl_release integrity tables

Build: https://github.com/daocuna46-alt/NAPO-ESP-PUBGM-DS-NOKING/actions/workflows/build.yml

## Todo
If still "runtime integrity verification failed": runtime-check with lldb,
breakpoint in qblDSCheckStartAuth (0x1000babb4) or hack start, inspect guard.
