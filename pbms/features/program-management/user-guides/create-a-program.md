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

# 📔 Create Program

Create Program screen helps to create a new program. This document provides step-by-step instructions to create a new program. The user with a Program Manager and Administrator role can create a new program.

## Prerequisites

The user must have a Program Manager role to create a new program.

Note:

Refer the [Create User and Assign Role](../../administration/role-based-access-control/user-guides/assign-roles-to-users.md) guide to know how to assign role for a User.

{% stepper %}
{% step %}
## Go to Programs

Click the main menu icon ![](../../../../.gitbook/assets/main-menu.png) and select _**Programs**_.&#x20;
{% endstep %}

{% step %}
## Edit Program

<img src="../../../../.gitbook/assets/programs.png" alt="Choose Programs in the menu" data-size="original">

<img src="../../../../.gitbook/assets/Program-screen.png" alt="Programs screen" data-size="original">

_**Programs**_ screen provides a dashboard view that lists all the available Program Names, Target Type, Number of Enrolled Beneficiaries against each program, State (whether active/inactive), and the Beneficiaries list.

In _**Programs**_ screen, the available features and their descriptions are:

<table><thead><tr><th width="130">Feature</th><th>Description</th></tr></thead><tbody><tr><td>Create</td><td>Click the <em><strong>Create</strong></em> button to create new program</td></tr><tr><td><img src="../../../../.gitbook/assets/download.png" alt="" data-size="original"></td><td>Click the <em><strong>Export All</strong></em> button to download the details in excel format</td></tr><tr><td>&#x3C;</td><td>Click the <em><strong>Left</strong></em> arrow to go the previous screen</td></tr><tr><td>></td><td>Click the <em><strong>Right</strong></em> arrow to go the next screen</td></tr><tr><td>Filters</td><td><p>Click the <em><strong>Filters</strong></em> link and select the appropriate options.</p><p>The valid values are:</p><ul><li>Archived</li><li>Add Customer Filter</li></ul><p>The advanced filter option allows you to define conditions and criteria to refine the search results.</p><ul><li>Select the <em><strong>Add Customer filter</strong></em> and then select the appropriate option in the first drop-down to display the specific data based on the option selected.</li><li>Select the criteria in second and third drop-down to refine the search results.</li><li>Click the <em><strong>Apply</strong></em> button to display the data based on the search</li></ul><p><em>Note: To enhance the search, click the <strong>Add a condition</strong> button and follows the steps given in <strong>Add Customer Filter</strong> option</em></p></td></tr><tr><td>Group By</td><td><ul><li>Click the <em><strong>Group By</strong></em> link, select <strong>Add Custom Group</strong> and then select the appropriate options in the drop-down to display the specific data based on the option selected.</li><li>Click the <em><strong>Apply</strong></em> button to display the data based on the search</li></ul></td></tr><tr><td>Favorites</td><td><ul><li><p>Click the <em><strong>Favorites</strong></em> link, select <strong>Save current search</strong> and then check the appropriate options. The valid values are:</p><ul><li>Use by default</li><li>Share with all users</li></ul></li><li>Click the <em><strong>Save</strong></em> button to display the data based on the search</li></ul></td></tr><tr><td>Search</td><td>This field is filled when the available option are selected in Filers, Group By, Favorites</td></tr></tbody></table>
{% endstep %}

{% step %}
## Create a  Program

Click the _**Create Program**_ button. The _**Set Program Settings**_ screen is displayed.



#### Set Program settings

In _**Set Program Settings**_ screen, the field and their descriptions are:

| Field                    | Description                                                                                            |
| ------------------------ | ------------------------------------------------------------------------------------------------------ |
| Program Name             | Enter the Program name                                                                                 |
| Target Type              | <p>Choose one of the Target Type. The valid values are:</p><ul><li>Groups</li><li>Individual</li></ul> |
| Currency                 | <p>Select the appropriate currency option. The valid values are:</p><ul><li>EUR</li><li>USD</li></ul>  |
| Is Reimbursement Program | Check the option if the reimbursement program is required                                              |

In _**Set Program Settings**_ screen, you can find the below tabs.

* [Configure the Default Eligibility Criteria](create-a-program.md#configure-the-default-eligibility-criteria)
* [Configure the Cycle Manager](create-a-program.md#configure-the-cycle-manager)
* [Configure the Entitlement Manager](create-a-program.md#configure-the-entitlement-manager)
* [PMT Configuration](create-a-program.md#pmt-configuration)
* [Map Portal Form](create-a-program.md#map-portal-form)
{% endstep %}

{% step %}
## **Configure the Default Eligibility Criteria**

Click the _**Configure the Default Eligibility Criteria**_ tab, the fields available in the tab are displayed.



<img src="../../../../.gitbook/assets/Set-Program-Settings-Eligibility Criteria.png" alt="Configure the Default Eligibility Criteria" data-size="original">

<table><thead><tr><th width="185">Field</th><th>Description</th></tr></thead><tbody><tr><td>Eligibility manager</td><td>Default option is selected by default</td></tr><tr><td>Admin Area</td><td>Enter the admin area</td></tr><tr><td>Filter</td><td></td></tr><tr><td>Match all records</td><td>Retrieves the data which matches all records</td></tr><tr><td><img src="../../../../.gitbook/assets/number-of-records.png" alt="" data-size="original"></td><td><p>Click the <em><strong>Records</strong></em> button. The <em><strong>Selected records</strong></em> screen is displayed.</p><p><em>Note:</em></p><ul><li><em>By default the list of three records are listed in the <strong>Selected records</strong> screen.</em></li><li><em>Click the <strong>Cancel</strong> button to close the <strong>Selected records</strong> screen.</em></li></ul></td></tr><tr><td><img src="../../../../.gitbook/assets/referesh-button.png" alt="" data-size="original"></td><td>Click the <em><strong>Refresh</strong></em> button to refresh the screen</td></tr><tr><td>Add filter</td><td><p>Click the <em><strong>Add filter</strong></em> button to set eligibility criteria using Domain Filters. You may set multiple eligibility criteria.</p><ol><li>Click the <em><strong>Add filters</strong></em> button. The multiple criteria fields are displayed.</li><li>Select the multiple criteria such as ID, condition and count.</li><li>Click the <strong>x</strong> button to remove the entry in the criteria fields.</li><li>Click the <strong>+</strong> button to add new multiple criteria field.</li><li>Click the <strong>...</strong> option to display fields in <em><strong>Any of</strong></em> section. The multiple criteria fields are displayed.</li></ol><p><em>Note: You can click the <strong>...</strong> option to add n number of <strong>Any of</strong> section</em></p><ol start="6"><li>The value chosen in the multiple criteria fields are displayed in the <em><strong>Code editor</strong></em>.</li><li>In the Match records chose one of the followings:</li></ol><ul><li>Select <em><strong>All</strong></em> to display the data belongs to <em><strong>All</strong></em> section</li><li>Select <em><strong>Any</strong></em> to display the data belongs to <em><strong>Any</strong></em> <em><strong>of</strong></em> section</li></ul></td></tr></tbody></table>

<img src="../../../../.gitbook/assets/Selected-records.png" alt="Selected records screen" data-size="original">
{% endstep %}
{% endstepper %}

