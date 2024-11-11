# Fuzzing on various properities

**The bullents**

- hidden prammeter
- hidden endpoint
- hidden file discovery

## How to Fuzz

There are various tools:

- FUFF
- KiteRunner
- IIS-Shortname-Scanner

## Fuzzig files and directories

Before fuzz, make sure that you can find an existing file, then fuzz. this method is called **Varify Method**.

```bash
GET /file.ext → 200
ffuf -w list -u "https://site.com/FUZZ" -ac
#use a list maker to generate a short list wlist_maker
```

Important note in fuzzing 

- make your own word list
- Fuzz based on the context, for example

        → Skip file fuzz on web app run by **Express**

        → Skip endpoint fuzzing on rest APIs (except the last part)

- Change the user-Agent header to avoid blocking
- Tune the treads to avoid banning
- Watch out the CDN before fuzzing

## Word list

you should generate your own word lists

Parameters → use that param extractor 

! extract parameters, filename, and words from AllUrls (gospider)

## Fuzzing endpoint

In order to fuzz an endpoint, use

- FFUF to fuzz last part of the endpoint
- KiteRunner to fuzz whole endpoint

```bash
kiterunner commamdns
```

## Fuzzing parameters

To fuzz on parameters, you can add bunch of parameters to speed up the fuzzing

```
GET /param1=value&param2=value2&param3=value3...
```

The following tools can be used to hidden parameters discovery

- Arjun
- x8 (is recommended)
- parameth (not tested)

## Where to fuzz?

Some cases are:

- Fuzz the endpoints which return information
- Fuzz the files without any parameter
- Fuzz all endpoint and files to discover extra parameters
- Root or other directories (files and directory fuzz)

## Methodology

I recommend to use the steps (Do not forget to use Verify Method)

- Crawl the target and save all file names and paths - Gospider and Manual crawling
- Detect the web app technologies, then

     → conduct fuzzing on the full and relative paths to discovery **hidden paths** 

     → conduct fuzzing on the file name and directories to discover **hidden files and directories**

     → generate a fuzz list based on the target’s site map and fuzz - ali.com/ali.com.bak

- Crawl the target and save all parameters - GAP, and gau-sorter
- conduct parameter fuzzing to discover hidden parameters

## Examples

Examples 1: a rest API endpoint

```
/api/user/699201852
```

Fuzz:

```
/api/user/69920852/**FUZZ** //words
/api/user/**FUZZ**/69920852 //words
/api/**FUZZ**/69920852/**FUZZ**
/api/user?**FUZZ**/69920852?**FUZZ**// params
```

Example 2: Single PHP page

```
/change_password.php
```

Fuzz

```
/**FUZZ**.php //file names, words
/change_password.php**FUZZ** // "~", ".1", ".2", ".3", "s"
/change_password.php?**FUZZ**
```

Some old extension

```bash
.7z, .back, .bak, .bck, .bz2, .copy, .gz, .old, .orig, .rar, .sav, .save, .tar, .tar.bz2, .gzip, .tar.gzip, .tgz, .tmp, .zip,
```

Fuzz on domain with old.txt

```bash
ali.com/ali.com.zip (tar|gzip|bz2|tar.zip|tgz|log)
ali.com/www.ali.com.zip
ali.com/ali.zip
```