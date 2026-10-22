[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on003029-blue)](https://doi.org/10.82901/nemar.on003029)

Fragility Multi-Center Retrospective Study
------------------------------------------

This dataset was updated and prepared for release as part of a manuscript by Bernabei & Li et al. (in preparation). A subset of the data has been featured in [1].

Summary
-------------

iEEG and EEG data from 5 centers is organized in our study with a total of 100 subjects. We publish 4 centers' dataset here due to data sharing issues. 

Acquisitions include ECoG and SEEG. Each run specifies a different snapshot of EEG data from that specific subject's session. For seizure sessions, this means that each run is a EEG snapshot around a different seizure event.

For additional clinical metadata about each subject, refer to the clinical Excel table in the publication.

Data Availability
----------------------

NIH, JHH, UMMC, and UMF agreed to share. Cleveland Clinic did not, so requires an additional DUA.

All data, except for Cleveland Clinic was approved by their centers to be de-identified and shared. All data in this dataset have no PHI, or other identifiers associated with patient. In order to access Cleveland Clinic data, please forward all requests to Amber Sours, SOURSA@ccf.org:

Amber Sours, MPH
Research Supervisor | Epilepsy Center
Cleveland Clinic  |  9500 Euclid Ave. S3-399 |  Cleveland, OH 44195
(216) 444-8638

You will need to sign a data use agreement (DUA).

Sourcedata
----------------

For each subject, there was a raw EDF file, which was converted into the BrainVision format with `mne_bids`.
Each subject with SEEG implantation, also has an Excel table, called `electrode_layout.xlsx`, which outlines where the clinicians marked each electrode anatomically. Note that there is no rigorous atlas applied, so the main points of interest are: `WM`, `GM`, `VENTRICLE`, `CSF`, and `OUT`, which represent white-matter, gray-matter, ventricle, cerebrospinal fluid and outside the brain. WM, Ventricle, CSF and OUT were removed channels from further analysis. These were labeled in the corresponding BIDS `channels.tsv` sidecar file as `status=bad`.
The dataset uploaded to `openneuro.org` does not contain the `sourcedata` since there was an extra
anonymization step that occurred when fully converting to BIDS.

Derivatives
----------------

Derivatives include:
* fragility analysis
* frequency analysis
* graph metrics analysis
* figures

These can be computed by following the following paper:
[Neural Fragility as an EEG Marker for the Seizure Onset Zone](https://www.biorxiv.org/content/10.1101/862797v3)

Events and Descriptions
-----------------------------------

Within each EDF file, there contain event markers that are annotated by clinicians, which may inform you of specific clinical events that are occuring in time, or of when they saw seizures onset and offset (clinical and electrographic). 

During a seizure event, specifically event markers may follow this time course:

	* eeg onset, or clinical onset - the onset of a seizure that is either marked electrographically, or by clinical behavior. Note that the clinical onset may not always be present, since some seizures manifest without clinical behavioral changes.
	* Marker/Mark On - these are usually annotations within some cases, where a health practitioner injects a chemical marker for use in ICTAL SPECT imaging after a seizure occurs. This is commonly done to see which portions of the brain are active metabolically.
	* Marker/Mark Off - This is when the ICTAL SPECT stops imaging.
	* eeg offset, or clinical offset - this is the offset of the seizure, as determined either electrographically, or by clinical symptoms.

Other events included may be beneficial for you to understand the time-course of each seizure. Note that ICTAL SPECT occurs in all Cleveland Clinic data. Note that seizure markers are not consistent in their description naming, so one might encode some specific regular-expression rules to consistently capture seizure onset/offset markers across all dataset. In the case of UMMC data, all onset and offset markers were provided by the clinicians on an Excel sheet instead of via the EDF file. So we went in and added the annotations manually to each EDF file. 

Seizure Electrographic and Clinical Onset Annotations
-----------------------------------------------------------------------------

For various datasets, there are seizures present within the dataset. Generally there is only one seizure per EDF file. When seizures are present, they are marked electrographically (and clinically if present) via standard approaches in the epilepsy clinical workflow.

Clinical onset are just manifestation of the seizures with clinical syndromes. Sometimes the maker may not be present.

Seizure Onset Zone Annotations
------------------------------
What is actually important in the evaluation of datasets is the clinical annotations of their localization hypotheses of the seizure onset zone.

These generally include:

	* early onset: the earliest onset electrodes participating in the seizure that clinicians saw
	* early/late spread (optional): the electrodes that showed epileptic spread activity after seizure onset. Not all seizures has spread contacts annotated.


Surgical Zone (Resection or Ablation) Annotations
-----------------------------------------------------------------------

For patients with the post-surgical MRI available, then the segmentation process outlined above tells us which electrodes were within the surgical removed brain region.

Otherwise, clinicians give us their best estimate, of which electrodes were resected/ablated based on their surgical notes.

For surgical patients whose postoperative medical records did not explicitly indicate specific resected or ablated contacts, manual visual inspection was performed to determine the approximate contacts that were located in later resected/ablated tissue. Postoperative T1 MRI scans were compared against post-SEEG implantation CT scans or CURRY coregistrations of preoperative MRI/post SEEG CT scans. Contacts of interest in and around the area of the reported resection were selected individually and the corresponding slice was navigated to on the CT scan or CURRY coregistration. After identifying landmarks of that slice (e.g. skull shape, skull features, shape of prominent brain structures like the ventricles, central sulcus, superior temporal gyrus, etc.), the location of a given contact in relation to these landmarks, and the location of the slice along the axial plane, the corresponding slice in the postoperative MRI scan was navigated to. The resected tissue within the slice was then visually inspected and compared against the distinct landmarks identified in the CT scans, if brain tissue was not present in the corresponding location of the contact, then the contact was marked as resected/ablated. This process was repeated for each contact of interest.

References
-----------------

[1] Adam Li, Chester Huynh, Zachary Fitzgerald, Iahn Cajigas, Damian Brusko, Jonathan Jagid, Angel Claudio, Andres Kanner, Jennifer Hopp, Stephanie Chen, Jennifer Haagensen, Emily Johnson, William Anderson, Nathan Crone, Sara Inati, Kareem Zaghloul, Juan Bulacio, Jorge Gonzalez-Martinez, Sridevi V. Sarma. Neural Fragility as an EEG Marker of the Seizure Onset Zone. bioRxiv 862797; doi: https://doi.org/10.1101/862797

[2] Appelhoff, S., Sanderson, M., Brooks, T., Vliet, M., Quentin, R., Holdgraf, C., Chaumon, M., Mikulan, E., Tavabi, K., Höchenberger, R., Welke, D., Brunner, C., Rockhill, A., Larson, E., Gramfort, A. and Jas, M. (2019). MNE-BIDS: Organizing electrophysiological data into the BIDS format and facilitating their analysis. Journal of Open Source Software 4: (1896). https://doi.org/10.21105/joss.01896

[3] Holdgraf, C., Appelhoff, S., Bickel, S., Bouchard, K., D'Ambrosio, S., David, O., … Hermes, D. (2019). iEEG-BIDS, extending the Brain Imaging Data Structure specification to human intracranial electrophysiology. Scientific Data, 6, 102. https://doi.org/10.1038/s41597-019-0105-7

[4] Pernet, C. R., Appelhoff, S., Gorgolewski, K. J., Flandin, G., Phillips, C., Delorme, A., Oostenveld, R. (2019). EEG-BIDS, an extension to the brain imaging data structure for electroencephalography. Scientific Data, 6, 103. https://doi.org/10.1038/s41597-019-0104-8

## BrainVision header sampling interval (19 Oct 2026)

In 41 of the 106 recordings the `.vhdr` header gave a sampling interval that did not match the sampling frequency of the sidecars (`*_ieeg.json` SamplingFrequency, channels.tsv sampling_frequency). The headers were written by pybv 0.2.0 (`;Written using pybv 0.2.0`), whose writer prints `SamplingInterval={}'.format(int(1e6 / sfreq))`: the interval in microseconds was truncated to an integer. Where 1e6 / sfreq is not a whole number, or is a hair below one (1e6 / 1000.0000000000001 = 999.9999999999999 -> 999), the header rate was wrong. Readers that take the rate from the header (MNE / mne_bids, EEGLAB, FieldTrip, EEGDash) used, for example, 1001.001 Hz instead of 1000 Hz for sub-jh104 and sub-jh106, so event times, durations and frequencies were off by up to 0.2 %.

Since 19 Oct 2026, `SamplingInterval` = 1e6 / SamplingFrequency of the run's `_ieeg.json`, written the way pybv 0.4.0 and later write it (`SamplingInterval={1e6 / sfreq}`; pybv 0.2.0 and 0.3.0 truncate), and as 1000 or 500 us where the sidecar value is 1000 or 2000 Hz plus floating-point noise (1000.0000000000001, 2000.0000000000002). Only that line changed; the rest of each header and the binary `.eeg` data are byte-for-byte unchanged.

| old SamplingInterval (rate read) | new SamplingInterval (rate read) | sidecar SamplingFrequency | runs |
|---|---|---|---|
| 1000 us (1000.000 Hz) | 1000.5882352941176 us (999.412 Hz) | 999.4121105232217 | 13: umf001 run-01, umf002 run-01, umf004 run-01, ummc005 run-01, ummc005 run-02, ummc007 run-01, ummc007 run-02, ummc007 run-03, ummc008 run-02, ummc008 run-03, ummc009 run-01, ummc009 run-02, ummc009 run-03 |
| 999 us (1001.001 Hz) | 1000 us (1000.000 Hz) | 1000.0000000000001 | 7: jh104 run-01, jh104 run-02, jh104 run-03, jh104 run-04, jh104 run-05, jh104 run-06, jh106 run-01 |
| 499 us (2004.008 Hz) | 500 us (2000.000 Hz) | 2000.0000000000002 | 3: pt17 run-01, pt17 run-02, pt17 run-03 |
| 2001 us (499.750 Hz) | 2001.172268907563 us (499.707 Hz) | 499.7071044492829 | 7: umf003 run-01, ummc001 run-01, ummc001 run-02, ummc001 run-03, ummc002 run-01, ummc002 run-02, ummc002 run-03 |
| 975 us (1025.641 Hz) | 975.9908256880735 us (1024.600 Hz) | 1024.5997950800408 | 1: umf005 run-01 |
| 4002 us (249.875 Hz) | 4002.344537815126 us (249.854 Hz) | 249.85355222464145 | 10: ummc003 run-01, ummc003 run-02, ummc003 run-03, ummc004 run-01, ummc004 run-02, ummc004 run-03, ummc006 run-01, ummc006 run-02, ummc006 run-03, ummc008 run-01 |

The sidecar rate is the right one. These checks were run on the files for every run: (1) `int(1e6 / SamplingFrequency)` gives exactly the old header value in all 41 runs; (2) events.tsv `sample` = round(onset x SamplingFrequency) in all 106 runs (at the old header rate, up to 196 samples off); (3) `RecordingDuration` = (number of samples - 1) / SamplingFrequency in every run whose `.eeg` is complete (37 of the 41).

These 41 `.vhdr` files were git-annex files. They are now plain git files, because the edited content has no annexed copy on the dataset storage.

## participants.json levels (19 Oct 2026)

The `Levels` of engel_score, ilae_score and ethnicity were keyed "1", "-1", ..., while participants.tsv stores "1.0", "-1.0", ...; the site levels were lower case ("jhh") while participants.tsv says "JHH". The bids-validator reported TSV_VALUE_INCORRECT_TYPE for these 4 columns. The keys now equal the values used in participants.tsv. The level descriptions and participants.tsv are unchanged.

## Known issues not fixed (19 Oct 2026)

- sub-umf002, sub-umf003, sub-umf004 and sub-umf005 (run-01): the `.eeg` file holds only 0.7 to 2.0 s of data (e.g. 690,980 bytes for 129 float32 channels, not a whole number of 516-byte samples), while RecordingDuration says 194 to 257 s and both events (onsets 131 to 188 s) lie beyond the end of the data. The released data files are truncated. Metadata edits cannot repair them.
- There is no electrodes.tsv (bids-validator IEEG_ELECTRODES_REQUIRED): electrode positions are not part of the release.
