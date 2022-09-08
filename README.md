# test-zenodo
Testing Zenodo releases.

This GitHub repository is linked to the test Zenodo record at: https://doi.org/10.5281/zenodo.6081432, which is updated based on the contents of Releases to this GitHub repository. The person updating the GitHub and creating Releases need not be the person who originally created the GitHub repository or linked it to Zenodo, as long as they have permission to push to the GitHUb repository. This ability to collaboratively update the Zenodo record is a key feature of these GitHub-based updates, and to our knowledge, is not possible using other methods of uploading data to Zenodo.

Metadata is stored in the .zenodo.json file, which is formatted based on documentation at https://developers.zenodo.org/, and was refined after testing various properties (see below).

## Results of testing various properties in .zenodo.json

To update metadata for the Zenodo record, update the corresponding properties in the .zenodo.json file, and then create a Release on GitHub. Based on previous tests, nothing will be updated on Zenodo until a GitHub Release is created, but the update happens almost instantaneously once that's been done (assuming the json contains valid metadata). 

Note that if .zenodo.json contains *anything* not recognized by Zenodo as valid, then the Release will fail to be posted to Zenodo, and will only succeed once the errors have been corrected and put into a new Release. See Release "version 0.0.5" for the most comprehensive list of .zenodo.json properties that have been tested here and found to be valid.

### Notes on specific properties

The following property triggers an automated request to the community owner to accept or reject the Zenodo record:
```
"communities": [{"identifier": "emerge-bii"}]
```

The following property is specific to the release under which it's specified (and therefore needs to be updated for each release, OR it can be omitted in order to default to the current date; also note that Zenodo does NOT check to ensure that this date is after the date of previous releases):
```
"publication_date": "2022-08-26"
```


### Known failed properties (do NOT add these to .zenodo.json; please update the list below if more are found)

The following properties were attempted to be added, but resulted in a failure to update the record on Zenodo:
```
"grants": [{"id": "10.13039/100000001::2022070"}]
```
(note: not sure if the EMERGE grant DOI above is valid, which may account for the failure-- it was generated based on the format at https://developers.zenodo.org/#representation, with the EMERGE grant number appended after the NSF funder DOI prefix; not sure how the "::" is intended to work)
