# Flight evidence — week of September 27, 2026

Iteration: Sunday, September 27 through Saturday, October 3, 2026.
Activity and analysis: [Daily_Log_2026-10-01.md](../Daily_Log_2026-10-01.md).

These are PX4 software-in-the-loop (SITL) simulator logs, not physical flight tests. Firmware: v1.17.0, commit `d6f12ad1c4f70ad3230afd7d86e971421e02fef4`.

| Archived file | Original size (bytes) | Evidence |
| --- | ---: | --- |
| [21_46_45.ulg.gz](21_46_45.ulg.gz) | 12,717,901 | First reference flight; 18.328 seconds of settled hover |
| [21_59_10.ulg.gz](21_59_10.ulg.gz) | 27,224,087 | Second reference flight; 38.536 seconds of settled hover; 30-second settled-hover check passed |

Log filename dates refer to October 1, 2026 UTC. The corresponding filename times in America/New_York are 17:46:45 and 17:59:10 EDT, also October 1. Daily activity records use the local date.

## Integrity and recovery

Both archives use lossless gzip compression. Decompression was checked byte-for-byte against each source ULog before upload. Original source files were retained. Compression keeps each archive within the GitHub browser upload limit.

From this folder, restore ULogs without deleting the archives:

```bash
gzip -dk 21_46_45.ulg.gz 21_59_10.ulg.gz
sha256sum 21_46_45.ulg 21_59_10.ulg
```

Expected SHA-256 of the decompressed originals:

```text
5f9e77284abd24e7551c378a9e9bbd60b263dcdcd4c237e8cd7c73c75f942adb  21_46_45.ulg
3051938fb6ed348e12295dfcfde1969e2a77c99139a1a484238ae12a3bd8607c  21_59_10.ulg
```

## Filing convention

Store flight evidence once in its Sunday-start weekly iteration folder. Dated daily logs link to that evidence; the Saturday closeout summarizes and links to it. Preserve original evidence and record any derived analysis separately. This week remains open until Saturday closeout.
