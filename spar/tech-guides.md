---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Tech Guides

### Persistent Entities in openg2p-spar-mapper-api

<table><thead><tr><th width="230">Name</th><th>Description</th></tr></thead><tbody><tr><td>id_fa_mapping</td><td>This is the table that contains the records for id (beneficiary Id) and fa (Financial Address) mapping<br><br>The ID is the Primary Key for this table - i.e. a beneficiary id can only have one record in this table (essentially mapped to one Financial Address)</td></tr></tbody></table>

### Persistent Entities in openg2p-spar-self-service-api

<table><thead><tr><th width="229">Name</th><th>Description</th></tr></thead><tbody><tr><td>dfsp_providers</td><td><ul><li>This is a table that contains metadata about Financial Service Providers.</li><li>Financial Service Providers need to be onboarded (or added) to this table. </li><li>Each DFSP Provider can attached with an "FA Construct Strategy", which will determine how the FA is constructed if this DFSP Provider is selected by the End-User.</li></ul></td></tr><tr><td>id_providers</td><td><ul><li>This is a table that contains metadata about Identity Providers (ID Providers). For example, the National ID System of the Country, Driving License, etc.</li><li>ID Providers need to be onboarded (or added) to this table.</li><li>Each ID Provider is linked to (one or more) <a href="broken-reference">Login Providers</a>.</li><li>Each ID Provider is attached with an "FA Construct Strategy", which will determine how the ID is constructed if the End-User logs in to SPAR using this ID Provider.</li></ul></td></tr><tr><td>fa_construct_strategy</td><td><ul><li>This is a string that describes how the FA or ID gets constructed. Which is present in the form of "{type}:{value}@{provider}".</li><li>For example, if FA Construct Strategy is "account_no:{acc_no}@{dfsp_provider_name}", the resultant FA will be "account_no:12345@bank1". <br>Whatever is given in curly braces "{x}" will be replaced by the relevant value.</li><li><p>For ID construction, the values will be taken from the Authentication response. The following are some of the fields that are usually available in Auth Response.</p><ul><li>sub - Subject. Usually the ID/Token.</li><li>iss - Issuer URL.</li><li>name - Name of the End-User.</li><li>email - Email of the End-User.</li><li>phone_number - Phone Number of the End-User.</li></ul></li><li>For FA construction, the values will be taken from the form submitted by the End-User. <br>This is a list of key-value pairs for each DFSP Level filled by the End-User, the key being the code of each DFSP Level and the value being the value filled.<br>Example [level1code: level1value, level2code: level2value].</li></ul></td></tr><tr><td>dfsp_levels</td><td><ul><li>This table contains information about different levels of inputs asked on the Update FA Request Form.</li><li><p>Each DFSP Level contains the following fields.</p><ul><li>name - Name to be displayed on the UI.</li><li>code - Code for this level, which can be used in FA Construct Strategy.</li><li>level - Integer that describes the position of this level among all levels of inputs that the End-User is asked for.</li></ul></li><li>If "level" is negative, it will considered as text input on the UI. Otherwise, it will considered as a dropdown where values are picked from DFSP Level Values.</li></ul></td></tr><tr><td>dfsp_level_values</td><td><ul><li>This table contains information about different values against each level of input asked on the Update FA Request Form.</li><li><p>Each DFSP Level Value contains the following fields.</p><ul><li>name - Name to be displayed on the UI.</li><li>code - Code for this level, which can be used in FA Construct Strategy.</li><li>level_id - The DFSP Level Entry to which this is a value of.</li><li>next_level_id (Optional) - The DFSP Level that is to be asked next if this Value is selected.</li><li>parent_id (Optional) - The DFSP Level Value, which was selected in the previous Level Input, that led to the selection of this Level Value.</li><li>dfsp_provider_id (Optional) - Each Level Value can be associated with a DFSP Provider, and the FA Construct Strategy will be derived from the DFSP Provider. <br>For example; if Bank is selected as "National Bank" in the form, then a DFSP Provider can be created for the National Bank and an FA Construct Strategy can be associated with this DFSP Provider.</li></ul></li></ul></td></tr></tbody></table>

### APIs

[Refer to Stoplight API documentation](https://openg2p.stoplight.io/docs/social-payments-account-registry)