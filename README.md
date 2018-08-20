<script src="https://cdn.plaid.com/link/v2/stable/link-initialize.js">
</script>
<script>
// Initialize Link with the `token` parameter
// set to the generated public_token for the Item
var linkHandler = Plaid.create({
  env: 'sandbox',
  clientName: 'Client Name',
  key: '[PUBLIC_KEY]',
  product: ['transactions'],
  token: '[GENERATED_PUBLIC_TOKEN]',
  onSuccess: function(public_token, metadata) {
    // You do not need to repeat the /item/public_token/exchange
    // process when a user uses Link in update mode.
    // The Item's access_token has not changed.
  },
  onExit: function(err, metadata) {
    // The user exited the Link flow.
    if (err != null) {
      // The user encountered a Plaid API error prior
      // to exiting.
    }
    // metadata contains information about the institution
    // that the user selected and the most recent API request
    // IDs. Storing this information is helpful for support.
  },
});
// Trigger the authentication view
document.getElementById('linkButton').onclick = function() {
  // Link will automatically detect the institution ID
  // associated with the public token and present the
  // credential view to your user.
  linkHandler.open();
};
</script>
