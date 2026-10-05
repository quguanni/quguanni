## Jenny Guanni Qu

I measure how long bugs survive in other people's code. Occasionally I shorten one.

### CVEs

| | | |
|---|---:|---|
| [CVE-2026-52986](https://www.cve.org/CVERecord?id=CVE-2026-52986) | 9.8 | linux · netfilter: nf_conntrack_sip |
| [CVE-2026-23455](https://www.cve.org/CVERecord?id=CVE-2026-23455) | 9.1 | linux · netfilter: nf_conntrack_h323, DecodeQ931() |
| [CVE-2026-23456](https://www.cve.org/CVERecord?id=CVE-2026-23456) | 8.2 | linux · netfilter: nf_conntrack_h323, decode_int() |
| [CVE-2026-31525](https://www.cve.org/CVERecord?id=CVE-2026-31525) | 7.8 | linux · bpf: interpreter sdiv/smod |
| [CVE-2026-43453](https://www.cve.org/CVERecord?id=CVE-2026-43453) | 7.1 | linux · netfilter: nft_set_pipapo |
| [CVE-2026-41254](https://www.cve.org/CVERecord?id=CVE-2026-41254) | 4.0 | little-cms · cmslut.c |
| CVE-2026-3890 | — | qemu · hw/usb/hcd-ohci *(reserved, unpublished)* |

One record names me. The rest cite commits that do.

### Linux

| | age at fix | |
|---|---:|---|
| [`1e3a3593162c`](https://github.com/torvalds/linux/commit/1e3a3593162c) | 20.0 yr | netfilter: nf_conntrack_h323: fix OOB read in decode_int() CONS case |
| [`f173d0f4c0f6`](https://github.com/torvalds/linux/commit/f173d0f4c0f6) | 20.0 yr | netfilter: nf_conntrack_h323: check for zero length in DecodeQ931() |
| [`00050ec08cec`](https://github.com/torvalds/linux/commit/00050ec08cec) | 18.5 yr | netfilter: xt_time: use unsigned int for monthday bit shift |
| [`94545ffc0ae8`](https://github.com/torvalds/linux/commit/94545ffc0ae8) | 11.3 yr | pnfs/flexfiles: validate ds_versions_cnt is non-zero |
| [`d6d8cd2db236`](https://github.com/torvalds/linux/commit/d6d8cd2db236) | 6.1 yr | netfilter: nft_set_pipapo: fix stack OOB read in pipapo_drop() |
| [`c77b30bd1dcb`](https://github.com/torvalds/linux/commit/c77b30bd1dcb) | 2.6 yr | bpf: fix undefined behavior in interpreter sdiv/smod for INT_MIN |
| [`4ac95c65efea`](https://github.com/torvalds/linux/commit/4ac95c65efea) | — | selftests/bpf: add tests for sdiv32/smod32 with INT_MIN dividend |

h323, xt_time and flexfiles were on a list Vidoc Security Lab gave me to triage; I confirmed
them and wrote the fixes. I found pipapo and bpf myself.

Found, then fixed by people who know the subsystem better than I do:
bpf [`bc308be380c1`](https://github.com/torvalds/linux/commit/bc308be380c1) ·
netfilter [`8cf6809cddcb`](https://github.com/torvalds/linux/commit/8cf6809cddcb)

### Elsewhere

**QEMU** — [`129922c2bc39`](https://github.com/qemu/qemu/commit/129922c2bc39) OHCI infinite loop on MPS=0 ·
[`cb1e8c18df62`](https://github.com/qemu/qemu/commit/cb1e8c18df62) sb16 VMState bounds.

**mihomo** — four protocol parsers that crashed on one packet:
[socks4](https://github.com/MetaCubeX/mihomo/commit/5184081ac327),
[vision TLS](https://github.com/MetaCubeX/mihomo/commit/dbaf85b71b22),
[trojan UDP](https://github.com/MetaCubeX/mihomo/commit/5bdb1cc7e1ee),
[quic sniffer](https://github.com/MetaCubeX/mihomo/commit/11848509fb13).

**FFmpeg** — found; fixed upstream:
[wmv2dec skip bits](https://github.com/FFmpeg/FFmpeg/commit/f73849887cb9) ·
[matroskadec sub_packet_h × frame_size](https://github.com/FFmpeg/FFmpeg/commit/f47ca0a5e6af) ·
[pngdec dead overflow check](https://github.com/FFmpeg/FFmpeg/commit/e7b4ddc9d6e3) ·
[alsdec abs(INT_MIN)](https://github.com/FFmpeg/FFmpeg/commit/1853c80e20c5).

**libtiff** — [OJPEG overflow](https://gitlab.com/libtiff/libtiff/-/issues/796) → [!843](https://gitlab.com/libtiff/libtiff/-/merge_requests/843) ·
[PixarLog overflow](https://gitlab.com/libtiff/libtiff/-/issues/797) → [!842](https://gitlab.com/libtiff/libtiff/-/merge_requests/842) ·
[YCbCr44 fromskew copy-paste](https://gitlab.com/libtiff/libtiff/-/issues/798) → [!838](https://gitlab.com/libtiff/libtiff/-/merge_requests/838).

**Little-CMS** — besides the CVE, a [MemoryWrite/MemoryRead overflow](https://github.com/mm2/Little-CMS/issues/542).
"Not required at all," said the maintainer, and [fixed it anyway](https://github.com/mm2/Little-CMS/commit/e33c55293fd8).

**libpng** — [#853](https://github.com/pnggroup/libpng/issues/853): a bug in the fix for CVE-2026-22695. Confirmed; fix pending.

**Artifex** — 26 bugs filed against Ghostscript, jbig2dec, MuPDF and GhostPDL. 2 wontfix, 1 invalid.
The invalid one was mine to own.

<details>
<summary>The fixed ones, each with its commit</summary>

| | | |
|---|---|---|
| [709206](https://bugs.ghostscript.com/show_bug.cgi?id=709206) | PDF filter-bomb protection bypass | [`fa78399a62e3`](https://github.com/ArtifexSoftware/ghostpdl/commit/fa78399a62e3) |
| [709209](https://bugs.ghostscript.com/show_bug.cgi?id=709209) | CMap heap overflow write | [`626c95688320`](https://github.com/ArtifexSoftware/ghostpdl/commit/626c95688320) |
| [709210](https://bugs.ghostscript.com/show_bug.cgi?id=709210) | Type 1 font buffer overread | [`1bf28caf5469`](https://github.com/ArtifexSoftware/ghostpdl/commit/1bf28caf5469) |
| [709211](https://bugs.ghostscript.com/show_bug.cgi?id=709211) | operator precedence defeats -dPDFSTOPONERROR | [`5f1a5c6ba3d6`](https://github.com/ArtifexSoftware/ghostpdl/commit/5f1a5c6ba3d6) |
| [709216](https://bugs.ghostscript.com/show_bug.cgi?id=709216) | save/restore offset truncation | [`6a7db6733bbc`](https://github.com/ArtifexSoftware/ghostpdl/commit/6a7db6733bbc) |
| [709218](https://bugs.ghostscript.com/show_bug.cgi?id=709218) | pdf_deref off-by-one and missing bounds | [`98ccff6f48eb`](https://github.com/ArtifexSoftware/ghostpdl/commit/98ccff6f48eb) |
| [709220](https://bugs.ghostscript.com/show_bug.cgi?id=709220) | image size int truncation | [`197acf6943eb`](https://github.com/ArtifexSoftware/ghostpdl/commit/197acf6943eb) |
| [709221](https://bugs.ghostscript.com/show_bug.cgi?id=709221) | ICC colorants heap overflow | [`20d70c20bf38`](https://github.com/ArtifexSoftware/ghostpdl/commit/20d70c20bf38) |
| [709223](https://bugs.ghostscript.com/show_bug.cgi?id=709223) | TrueType refcount use-after-free | [`b89fbc34e68e`](https://github.com/ArtifexSoftware/ghostpdl/commit/b89fbc34e68e) |
| [709224](https://bugs.ghostscript.com/show_bug.cgi?id=709224) | font length int64 → int truncation | [`b196360ff32c`](https://github.com/ArtifexSoftware/ghostpdl/commit/b196360ff32c) |
| [709225](https://bugs.ghostscript.com/show_bug.cgi?id=709225) | packedarray fix that didn't (Bug 701550) | [`8d2d9461dc43`](https://github.com/ArtifexSoftware/ghostpdl/commit/8d2d9461dc43) |
| [709226](https://bugs.ghostscript.com/show_bug.cgi?id=709226) | legacy scan converter overflows | [`7a3f04e7f204`](https://github.com/ArtifexSoftware/ghostpdl/commit/7a3f04e7f204) |
| [709361](https://bugs.ghostscript.com/show_bug.cgi?id=709361) | MuPDF: TTF cmap out-of-bounds read | [`e22271f99911`](https://github.com/ArtifexSoftware/mupdf/commit/e22271f99911) |
| [709364](https://bugs.ghostscript.com/show_bug.cgi?id=709364) | MuPDF: CFF INDEX out-of-bounds read | [`611f75f0c865`](https://github.com/ArtifexSoftware/mupdf/commit/611f75f0c865) |
| [709365](https://bugs.ghostscript.com/show_bug.cgi?id=709365) | MuPDF: CFF charset out-of-bounds read | fixed |

Two more were real, but someone had filed them first: [709362](https://bugs.ghostscript.com/show_bug.cgi?id=709362), [709363](https://bugs.ghostscript.com/show_bug.cgi?id=709363).

</details>

### Measurement

125,183 bug-fix pairs across twenty years of kernel history. Median survival 0.7 years, mean
2.1, and 13.5% last past five. I published that in January and fixed two twenty-year-olds in
March, which I submit as supporting evidence.

[kernel-vuln-data](https://github.com/quguanni/kernel-vuln-data) ·
[kernel-archaeology](https://github.com/quguanni/kernel-archaeology)

### Detection

VulnBERT. Eight versions, six months, 91.4% recall at 5.9% false positive over 650K commits on
a strict temporal split. The version that worked is the previous architecture with better
negative sampling, which was not the lesson I was hoping for. Contrastive learning ran
beautifully on 4K samples and returned NaN at 162K.

### Talks

[**Why Most ML Vulnerability Detection Fails**](https://github.com/quguanni/talks/tree/main/unprompted-2026)
· [un]prompted, March 2026 ([recording](https://www.youtube.com/watch?v=93jhfuL-ndo)).
Before training anything I built nine ways to cheat. Bag-of-words reaches 0.825 AUC. At 512
tokens a transformer is reading your commit message, not your code.

[**How Long Linux Kernel Bugs Actually Hide**](https://github.com/quguanni/talks/tree/main/bugbash-2026)
· BugBash, April 2026 ([recording](https://quguanni.com/talks)). Lightning talk. A correctness
conference full of people building better ways to catch bugs; this was the measurement instead.

> The hard problem is detecting what isn't there.

---

[quguanni.com](https://quguanni.com) · [@GuanniQu](https://x.com/GuanniQu) · jenny@quguanni.com
