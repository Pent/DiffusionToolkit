# Table of Contents

* [Searching](#searching)
* [Advanced Searching](#advanced-searching)

# Searching

Searching is performed by checking if the prompt contains the search term.  Separate search terms using a comma. Each search term is ANDed to produce the final filter. 

For example:

```
A man staring into a starry night sky, by Van Gogh
```

will match prompts that contain both `A man staring into a starry night sky` AND `by Van Gogh` in any order or position.

If you want to match an exact term that contains a comma, place the term in double quotes:

```
"A man staring into a starry night sky, by Van Gogh"
```

will match prompts that contain ONLY `A man staring into a starry night sky, by Van Gogh` in that exact wording.

Note that spaces are important.

```
"A man staring into a starry night sky , by Van Gogh"
```

will not match the previous term.


# Advanced Searching

You can also include image generation parameters in your search query. 

Add the parameters to the end of your query, e.g:

```
A man staring into a starry night sky, by Van Gogh steps: 20 cfg:12  
```

Parameters will be ANDed, meaning adding more parameters will filter out more results. 

The following parameters are supported:

* `steps:<number>`, `steps:<start>-<end>`

* `sampler:<name>` 

  Sampler names can be a bit tricky, as they vary from one tool to another. This means we need to know what the samplers are in advance, so we can expect them (and not accidentally try to use the next parameter name as part of the sampler search). The `samplers.txt` file contains a list of known samplers. (If these are incorrect, let me know).

  * Euler a or `euler_a`
  * Euler or `euler`
  * LMS or `lms`
  * Heun or `heun`
  * DPM2 or `dpm2`
  * DPM2 a or `dpm2_a`
  * DPM++ 2S a or `dpm++_2s_a`
  * DPM++ 2M or `dpm++_2m`
  * DPM++ SDE or `dpm++_sde`
  * DPM fast or `dpm_fast`
  * DPM adaptive or `dpm_adaptive`
  * LMS Karras or `lms_karras`
  * DPM2 Karras or `dpm2_karras`
  * DPM2 a Karras or `dpm2_a_karras`
  * DPM++ 2S a Karras or `dpm++_2s_a_karras`
  * DPM++ 2M Karras or `dpm++_2s_karras`
  * DPM++ SDE Karras or `dpm++_sde_karras`
  * DDIM or `ddim`
  * PLMS or `plms`
  
  So if a new sampler comes out, and the toolkit isn't updated, just add it to `samplers.txt`

* `cfg:<number>` or `cfg_scale:<number>` or `cfg scale:<number>`

* `seed:<number>`

* `size:<width>x<height>` or `size:<width>:<height>` 
  
  `width` and `height` can be a number or a question mark (`?`) to match any value. e.g. `size:512x?` 

* `model_hash:<hash>`

* `aesthetic_score: [<|>|<=|>=|<>] <number>`

  You can search for an exact number e.g. `aesthetic_score: 0.6`, but most likely you would like to do a comparative search such as less than `aesthetic_score: < 0.6`

* `hypernet: <name>`

* `hypernet strength: [<|>|<=|>=|<>] <number>`

* `date:`

  Allows you to search by the file's created date

  * `date: today` - Include files from the current date  
  * `date: yesterday` - Include files from the previous date  
  * `date: between 11-11-2022 and yesterday` - Include files from November 11, 2022 the previous date  
  * `date: from 10-10-2022 to 11-11-2022` - alternate syntax
  * `date: before 11-11-2022` - Include files since the beginning of time, up to November 11, 2022
  * `date: since 01-01-2022` - Include files created on January 1, 2022 up to today

  Notes:

  * `YYYY-MM-DD` format is supported
  * `XX-XX-XXXX` dates will be parsed using your computer's date format, i.e. 
`MM-DD-YYYY` for US and similar regions, `DD-MM-YYYY` for European regions.



## Notes

* The parameters e.g. `steps:`, `sampler:` are not case sensitive. You can use `Steps:`, `Sampler:`, so you can copy it from a prompt.
* You can have 0 or more spaces *after* the colon (`:`) and before the parameter value.
  * e.g. `steps:20`, `steps: 20`, `steps:   20` are OK
  * but `steps  :20`, `steps :20` are not

## Search on Multiple Values 

You can search on multiple values on most parameters. The results will be ORed, meaning adding more values will add more results.

* You can specify a range for seed with `seed:<start>-<end>`
  * e.g. `seed:10000-20000`
* You can specify mutiple values for other parameters using a pipe (`|`) 
  * e.g. `sampler: euler a | ddim | plms`
  * e.g. `cfg: 4.5 | 7 | 9 | 12`
  * e.g. `model_hash: aabbccdd | deadbeef | 12345678`