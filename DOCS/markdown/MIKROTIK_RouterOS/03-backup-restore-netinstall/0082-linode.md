## Linode 

When creating multiple Linodes with the same disk size, new Linodes will have the same systemID. This will cause issues to get a Trial/Paid license. To avoid this, run the command `/system license generate-new-id` after the first boot and before you request a trial or paid license. This will make sure the ID is unique.
