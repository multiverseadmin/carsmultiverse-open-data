# CarsMultiverse open data mirror

A nightly copy of the open datasets published by [CarsMultiverse](https://carsmultiverse.com/), an independent site that keeps every version of a vehicle recall notice and notices when the wording changes.

**The site is the source. This repository is a mirror.** If the two ever differ, the site is right and this copy is behind.

CarsMultiverse is not an authority. The recall notices are published by NHTSA (United States), Transport Canada and the European Commission's Safety Gate. Their wording belongs to them. What CarsMultiverse adds is the record of when each notice was read, how it was fingerprinted, and what changed between readings.

## What is here

`data/` holds one file per dataset, refreshed every night at 03:40 UTC by the workflow in `.github/workflows/mirror.yml`:

- `data/{id}.csv` and `data/{id}.json` for each dataset the site lists on its [data page](https://carsmultiverse.com/data/). Today that is twelve datasets: the register of American campaigns, the rewrites caught, the delay studies, the completion study, the Canadian and European crosswalks and the three-register cases.
- `data/register-index.json`: one row per American campaign with a fingerprint of its defect, consequence and remedy text, the dates of the first and last reading, and the number of rewrites seen.
- `data/changes.json`: every rewrite caught, with the fingerprints before and after.
- `data/datasets-index.json`: the site's own list of datasets, as fetched.

`CHANGELOG.md` gets one line for every night on which any file changed, with the date and the row counts.

## Why the commit history matters

Every commit is a timestamped copy of what the site published that night, signed by GitHub's own clock rather than ours. That makes this repository a second proof of custody. If a notice is rewritten and someone later doubts when the change was caught, the commit that first carried the new fingerprint is independent evidence. Use `git log -p -- data/register-index.json` to walk it.

## Licence

The site's own fields, meaning the fingerprints, reading dates, counts, study results and the structure of the files, are released under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). See `LICENSE-DATA.md`.

The text of the recall notices themselves is published by NHTSA, Transport Canada and the European Commission and remains theirs. CarsMultiverse does not claim it and neither does this repository.

## How to cite

> CarsMultiverse, *{dataset name}*, read on {date}. https://carsmultiverse.com/data/ (mirror: this repository, commit {hash}).

Quote the commit hash when a date matters. The site's own [cite this site](https://carsmultiverse.com/for-journalists/) page has a format for individual campaigns and changes.

## What we ask

- A visible credit, "Data from CarsMultiverse", with a link.
- No implication that the site or this mirror is an authority. Link to the register's own notice when you can.
- Tell us where the data went, through the [contact page](https://carsmultiverse.com/contact/), so we can link back and warn you if we correct something.

## Corrections

Errors in the data are corrected on the site first and logged on its [corrections page](https://carsmultiverse.com/corrections/). The next nightly run brings the correction here. Please do not open pull requests against `data/`; the workflow would overwrite them.
