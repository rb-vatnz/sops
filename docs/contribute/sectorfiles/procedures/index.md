---
title: Overview
---

--8<-- "includes/abbreviations.md"

!!! warning
    Procedures are **not** automatically pulled from the ANR, due to incomplete data and differing formats. These must be updated in line with the ANR.

The Procedure Editor provides an easy-to-use interface for creating and editing procedures for the aerodromes contained within the database.

The Procedure Editor covers the following procedures -

* SIDs
* STARs
* VFR arrivals and departures
* Helicopter-specific procedures (not used)
* Approaches (RNP, RNP-AR, LOC and VOR)

<figure markdown> 
  ![Procedure Editor Main Screen](assets/../../assets/ProcEdMainScreen.png){ width="600" }
</figure>

## How does it work?

The ProcEd allows the user to create procedures for any of the aerodromes contained within the `contl_apt` or `uncontl_apt` tables. Aerodromes not appearing in either of these two tables will not be able to have procedures created for them - whether they appear in other tables or not, such as `ap_aids`.

After an aerodrome has been added to either of the required tables, it will show under the `Airport ICAO` dropdown when ++"New Procedure"++ is clicked. The app will automatically pull in the aerodrome's runways, as listed in the `runway` table.

For procedures that have transitions (SIDs, STARs and approaches), you are required to add the base procedure, and then the various transition routes. This is further defined in the various procedure sections.

We have chosen not to model helicopter procedures in New Zealand, due to there are not many helicopter procedures in use around the country; and where helicopter procedures *do* exist, they are relatively short.

## What happens on export?

On export, the ProcEd largely performs the same actions for both the vatSys and EuroScope releases, but performs and exports them slightly differently. 

### vatSys

* Each Aerodrome in the `contl_apt` and `uncontl_apt` tables are given their own Map folder within the `Maps` dropdown. The file name `XX_ACU` is dictated by the `icaoabbrv` in the relevant table.
* All the SIDs, STARs and approaches are rendered on their own map layer, sorted by runway. RNP and RNP-AR approaches are given their own map layers, also sorted by runway.
    * These are also given custom colours, but these are better explained in the individual procedure sections.
* All VFR arrivals and departures are also given their own map layer, independent of the VRP map layer.

### Euroscope

* All procedure layers are rendered into the SIDSTAR section, and are sortable by ICAO. VFR procedures are also rendered in this section.

## Procedural Waypoints

There are three types of IFR waypoints in use in the dataset: IFR Significant Points, ICAO 5LNCs and Procedural/Terminal waypoints. Procedural waypoints are used in Aerodrome procedures where there is no need for a named waypoint. 

These waypoints typically follow the format: `XXYYY`, where `XX` is the Aerodrome, and `YYY` are three numbers. For example, the `QN760`, `QN745` and `QN741` waypoints on the `RNP Z Rwy 23 (AR)` approach into NZQN.

These fixes are not listed in the ANR, and depending on the type of procedure, often don't have their coordinates listed on the plate.

If you attempt to create a procedure with a procedural waypoint that is not present in the database, you will receive an error, and be notified to [manually define the waypoint using this process](../datamanagement/ManualDefinitions.md#manual-ifr-waypoint-definitions).

## Threshold Fixes

In the dataset, custom fixes have been created for each threshold of a runway. These are generated from the runway data provided by the ANR, and don't require any manual attention by the user.

They usually follow the format of `XXYYT` - where `XX` is the two letter ICAO abbreviation, `YY` is the runway identifier, and `T` denotes the threshold. For example, `PM07T` and `PM25T` denote the thresholds for Palmerston North's single runway.  

Where a runway has an R/L designation, the designator will replace the `T`. For example, `AA23L` and `AA05R` denote the thresholds for Auckland.

These are mostly used in SIDs, where an origination point is required. These used to be used for approach procedures, but are now appended automatically by the SFG upon dataset export.

## Exporting a discrete map for a Procedure

It is possible to export a separate map layer for a single procedure. This can be helpful for when you want to illustrate changes in procedures to the Dataset's users, and exports the procedure exactly how it would normally be seen within an aerodrome's ACU map layer.

To do this, navigate to the procedure you wish to export in the Procedure Editor, and click on the yellow ++"Create map for selected procedure"++ button. You will then be prompted that the file has been exported, and you will be alerted to this file's location.

!!! important
    When exporting the procedure, the file name will be set to the procedure's name, **however** the map layer's name is not. You will need to manually edit all `Name` attributes within the file to another name, such as the procedure name. 

