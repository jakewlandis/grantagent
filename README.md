# grantagent
# API documentation for connecting Agentforce in Salesforce to Grants.gov via Mulesoft

## There are two designs in this repository.

The first is designed to retrieve a list of grant funding opportunities.
The second is designed to retrieve the details of a specific opportunity.

## Retrieiving a list of grant funding opportunities: 
### This is an openapi 3.0 implementation designed to retrieve 10 grant opportunities from grants.gov using their open 'search2' API. (https://www.grants.gov/api/api-guide)

When tied to a Mulesoft instance, this API format returns the first 10 results for a given keyword or series of pipe-delimited keywords in a format designed for use with Agentforce.

Example:
https://[mulesoftendpoint]/grantgov?e=Chemistry

Returns:
```
{
    "opportunity0": "356055 | Computational and Data-Enabled Science and Engineering | National Science Foundation",
    "opportunity1": "341244 | Division of Chemistry: Disciplinary Research Programs: No Deadline Pilot | National Science Foundation",
    "opportunity2": "347329 | Electrochemical Systems | National Science Foundation",
    "opportunity3": "350841 | Blueprint Neurotherapeutics Network (BPN): Small Molecule Drug Discovery and Development for Disorders of the Nervous System (U44 Clinical Trial Optional) | National Institutes of Health",
    "opportunity4": "320490 | Environmental Engineering | National Science Foundation",
    "opportunity5": "356531 | Blueprint Neurotherapeutics Network (BPN): Small Molecule Drug Discovery and Development of Disorders of the Nervous System (UG3/UH3 Clinical Trial Optional) | National Institutes of Health",
    "opportunity6": "344128 | Avenir Award Program for Chemistry and Pharmacology of Substance Use Disorders (DP1- Clinical Trial Not Allowed) | National Institutes of Health",
    "opportunity7": "329436 | University Nuclear Leadership Program&ndash; Scholarship and Fellowship Support | Idaho Field Office",
    "opportunity8": "357934 | Fiscal Year (FY) 2025 Directors' Research Initiative (DRI) | Air Force Office of Scientific Research",
    "opportunity9": "358300 | Research, Development, and Training in Isotope Production | Office of Science"
}
```

This data is returned as a single object as Mulesoft Topics for Agentforce does not accept arrays.  This design allows us to present the user with options for further investigation or use in their Salesforce org.


## Retrieving the details of a specific opportunity:
### This is an openapi 3.0 implementation designed to retrieve 10 grant opportunities from grants.gov using their open 'fetchOpportunity' API. (https://www.grants.gov/api/api-guide)

When tied to a Mulesoft instance, this API format returns the title, agency, synopsis, response date and url of an opportunity in a format designed for use with Agentforce.

Example:
https://[mulesoftendpoint]/grantgovdetail?opp=356530

Returns:
```
{
    "title": "BRAIN Initiative: Reagent Resources for Brain Cell Type-Specific Access to Broaden Distribution of Enabling Technologies for Neuroscience (U24 Clinical Trial Not Allowed)",
    "agencyName": "National Institutes of Health",
    "synopsis": "This Notice of Funding Opportunity Announcement (NOFO) from the NIH Brain Research through Advancing Innovative Neurotechnologies (BRAIN) Initiative is intended to support establishment of facilities at minority-serving institutions (MSIs) and Institutional Development Award (IDeA)-eligible institutions for scaled production and distribution of brain cell type-specific access and manipulation reagents. Reagents will be initially developed in pilot resource projects for brain cell type-specific access and manipulation across vertebrate species from the BRAIN Initiative Armamentarium project. Awardees under this NOFO will work with the other Armamentarium awardees to manufacture and distribute the resources for use throughout the neuroscience community. It is envisioned that the awardees will work both with the Armamentarium community as well as with the neuroscience research community to optimize the use of new reagents. The types of reagents to be produced and distributed could include but are not limited to viral vectors, nucleic acid constructs, and nanoparticles designed for selective access to and manipulation of brain cell types. Such reagents will enable neuroscientists to probe circuit function with high precision in experimental animals and ex vivo human tissue and cells. Facilities are needed to contribute to the production and distribution of BRAIN Initiative Armamentarium project reagents broadly to neuroscience users.",
    "responseDate": "Jun 15, 2027 12:00:00 AM EDT",
    "url": "http://grants.nih.gov/grants/guide/rfa-files/RFA-MH-26-120.html"
}
```
