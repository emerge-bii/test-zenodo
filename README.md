# test-zenodo
Testing Zenodo releases.

This GitHub repository is linked to the test Zenodo record at: https://doi.org/10.5281/zenodo.6081432, which is updated based on the contents of Releases to this GitHub repository.

The person updating the GitHub and creating Releases need not be the person who originally created the GitHub repository or linked it to Zenodo, as long as they have permission to push to the GitHub repository. This ability to collaboratively update the Zenodo record is a key feature of these GitHub-based updates, and to our knowledge, is not possible using other methods of uploading data to Zenodo.

Metadata is stored in the .zenodo.json file, which is formatted based on documentation at https://developers.zenodo.org/, and was refined after testing various properties (see below).


## Specific instructions and test results for .zenodo.json properties

To update metadata for the Zenodo record, update the corresponding properties in the .zenodo.json file, and then create a Release on GitHub.  Based on previous tests, nothing will be updated on Zenodo until a GitHub Release is created, but the update happens almost instantaneously once that's been done (assuming the json contains valid metadata).

Note that if .zenodo.json contains *anything* not recognized by Zenodo as valid, then the Release will fail to be posted to Zenodo, and will only succeed once the errors have been corrected and put into a new GitHub Release. Unfortunately, just editing the Release to point to a new tagged commit doesn't appear to have any effect on Zenodo, even if the Release has not yet been pushed there (or, if it *has* been pushed to Zenodo but with incorrect metadata, then updating the GitHub release to point to a different tag will simply create conflicting versions between GitHub and Zenodo; this practice is therefore strongly discouraged). However, once a corrected Release has been made, it should still be possible to delete the old failed one on GitHub to keep things tidy. You can also use the "pre-release" checkbox on GitHub to indicate releases that are still in the testing phase (and then uncheck this box later), as this checkbox appears to have no effect on Zenodo.

Note on versioning: Zenodo gets the version numbers from the "version" property in .zenodo.json, and ignores any version numbers put into git tags or GitHub release names. Although this can be annoying (as it requires the user to update the version number in multiple places), it can be a useful feature for updating metadata in cases where the data itself was not changed, as the metadata can be updated and put into a new Zenodo release without having to increment the dataset's version number via the JSON.

For the most comprehensive list of .zenodo.json properties that have been tested here and found to be valid, please see the latest (non-pre) Release here that also appears on the Zenodo page. In addition, version 0.0.7 also contains an optional custom "publication_date", which has been removed from subsequent releases to simplify their publication. Past releases that failed to post to Zenodo (or that posted incorrectly) will be marked as such in this GitHub repository after the fact, but there may be a short delay before this happens.


### Notes on specific properties

The following property triggers an automated request to the community owner to accept or reject the Zenodo record:
```
"communities": [{"identifier": "emerge-bii"}]
```

The following property is specific to the release under which it's specified (and therefore needs to be updated for each release, OR it can be omitted in order to default to the current date; also note that Zenodo does NOT check to ensure that this date is after the date of previous releases):
```
"publication_date": "2022-08-26"
```

The "license" property is parsed separately from any license file that you may have added to your GitHub repository, and generates a link to the license URL on the Zenodo page. Therefore, you'll need to manually make sure that the license identifier in the JSON matches the license file in your GitHub repository. In addition, license identifiers on Zenodo follow a controlled vocabulary. To find the identifier of the license you are using, first see if it exists in either the license text, in the license URL, or elsewhere on the license webpage. Then test it by replacing "gpl-3.0" in the URL "https://zenodo.org/api/licenses/gpl-3.0" with the identifier that you found for your license, and then go to that URL in your browser. If you get a 404 message with "PID does not exist," then the license ID is invalid. But if you instead get a bunch of license details, then you can safely add the following property to .zenodo.json (again replacing "gpl-3.0" with your license identifier):
```
"license": "gpl-3.0"
```


### Known failed properties (do NOT add these to .zenodo.json; please update the list below if more are found)

The following properties were attempted to be added, but resulted in a failure to update the record on Zenodo:
```
"grants": [{"id": "10.13039/100000001::2022070"}]
```
(note: not sure if the EMERGE grant DOI above is valid, which may account for the failure-- it was generated based on the format at https://developers.zenodo.org/#representation, with the EMERGE grant number appended after the NSF funder DOI prefix; not sure how the "::" is intended to work)
