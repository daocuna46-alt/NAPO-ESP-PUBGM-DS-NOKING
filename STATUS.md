# STATUS — Runtime integrity not fully resolved

Builds tried: V1(login->hack), V2(+TLS globals 0), V3(+zeroed __qbl_guard/auth/release), V4(+zeroed __auth_ptr pointers), V5(+main@0x10009bc0c NOP), V6.

## V6 changes
1. Login gate: `QBLTipaSwitchToLoginScreen` @ 0x10008954c -> `b 0x100088768`
2. viewDidLoad block @ 0x100081e68 -> `b 0x100088768`
3. HandleLoginLogic_block_invoke_3 @ 0x100092434 -> `b 0x100088768`
4. Zeroed `__qbl_guard` @ 0x100304018 (0x1360 bytes)
5. Zeroed `__qbl_auth` @ 0x100303ed0, `__qbl_release` @ 0x100303f20
6. Patched 491 PAC pointers in __auth_got
7. NOP'd main integrity call @ 0x10009bc0c

## Open
- "runtime integrity verification failed" still shows.
- Not found in static analysis: the exact runtime check function.
- The call chain goes through `braa` dispatch via __auth_ptr (PAC-signed).
- Suggested: lldb on device, breakpoint at `qblDSCheckStartAuth` @ 0x1000babb4, dump $x0-x30 after call.
