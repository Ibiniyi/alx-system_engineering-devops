0x16. API advanced
listings
Many endpoints on reddit use the same protocol for controlling pagination and filtering. These endpoints are called Listings and share five common parameters: after / before, limit, count, and show.

Listings do not use page numbers because their content changes so frequently. Instead, they allow you to view slices of the underlying data. Listing JSON responses contain after and before fields which are equivalent to the "next" and "prev" buttons on the site and in combination with count can be used to page through the listing.

The common parameters are as follows:

after / before - only one should be specified. these indicate the fullname of an item in the listing to use as the anchor point of the slice.
limit - the maximum number of items to return in this slice of the listing.
count - the number of items already seen in this listing. on the html site, the builder uses this to determine when to give values for before and after in the response.
show - optional parameter; if all is passed, filters such as "hide links that I have voted on" will be disabled.
To page through a listing, start by fetching the first page without specifying values for after and count. The response will contain an after value which you can pass in the next request. It is a good idea, but not required, to send an updated value for count which should be the number of items already fetched.

modhashes
A modhash is a token that the reddit API requires to help prevent CSRF. Modhashes can be obtained via the /api/me.json call or in response data of listing endpoints.

The preferred way to send a modhash is to include an X-Modhash custom HTTP header with your requests.

Modhashes are not required when authenticated with OAuth.

fullnames
A fullname is a combination of a thing's type (e.g. Link) and its unique ID which forms a compact encoding of a globally unique ID on reddit.

Fullnames start with the type prefix for the object's type, followed by the thing's unique ID in base 36. For example, t3_15bfi0.


