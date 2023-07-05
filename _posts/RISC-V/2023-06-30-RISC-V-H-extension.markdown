---
layout: post
title:  "RISV-V Hypervisor Extension"
comments: true
categories: intel
published: true
date:   2023-06-30 04:10:41
---

The RISC-V hypervisor extension virtualizes the supervisor-level architecture to support the efficient hosting of guest operating systems atop a type-1 or type-2 hypervisor.
The hypervisor extension changes supervisor mode into hypervisor-extended supervisor mode (HS-mode, or hypervisor mode for short), where a hypervisor or a hosting-capable
operating system runs. The hypervisor extension also adds another stage of address translation, from guest physical addresses to supervisor physical addresses, to virtualize
the memory and memory-mapped I/O subsystems for a guest operating system.HS-mode acts the same as S-mode, but with additional instructions and CSRs that control the new
stage of address translation and support hosting a guest OS in virtual S-mode (VS-mode). Regular S-mode operating systems can execute without modification either in HS-mode
or as VS-mode guests.

In HS-mode, an OS or hypervisor interacts with the machine through the same SBI as an OS normally does from S-mode. An HS-mode hypervisor is expected to implement the SBI
for its VS-mode guest.

The current virtualization mode, denoted V, indicates whether the hart is currently executing in a guest. When V=1, the hart is either in virtual S-mode (VS-mode), or in
virtual U-mode (VU-mode) atop a guest OS running in VS-mode. When V=0, the hart is either in M-mode, in HS-mode, or in U-mode atop an OS running in HS-mode. The
virtualization mode also indicates whether two-stage address translation is active (V=1) or inactive (V=0).
![privileged](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/risc-v/risc-v-privileged.jpg)


An OS or hypervisor running in HS-mode uses the supervisor CSRs to interact with the exception, interrupt, and address-translation subsystems. Additional CSRs are provided
to HS-mode, but not to VS-mode, to manage two-stage address translation and to control the behavior of a VSmode guest: hstatus, hedeleg, hideleg, hvip, hip, hie, hgeip,
hgeie, henvcfg, henvcfgh, hcounteren, htimedelta, htimedeltah, htval, htinst, and hgatp.
![CSR](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/risc-v/risc-v-CSR.png)