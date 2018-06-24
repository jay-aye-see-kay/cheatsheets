# Default resource actions
These are good default routes for controlling a resource in a CRUD app like a photo in the example below from https://laravel.com/docs/5.5/controllers#resource-controllers.

_Note PUT should be used for complete updates and PATCH for partial updates, PUT is simpler to implement an should probably be used in most cases._
<table>
<thead>
<tr>
<th>Verb</th>
<th>URI</th>
<th>Action</th>
<th>Route Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>GET</td>
<td><code>/photos</code></td>
<td>index</td>
<td>photos.index</td>
<td>List all or a subset of photos</td>
</tr>
<tr>
<td>GET</td>
<td><code>/photos/create</code></td>
<td>create</td>
<td>photos.create</td>
<td>Show the form to create a new photo</td>
</tr>
<tr>
<td>POST</td>
<td><code>/photos</code></td>
<td>store</td>
<td>photos.store</td>
<td>Store the given photo</td>
</tr>
<tr>
<td>GET</td>
<td><code>/photos/{id}</code></td>
<td>show</td>
<td>photos.show</td>
<td>Show the specified photo</td>
</tr>
<tr>
<td>GET</td>
<td><code>/photos/{id}/edit</code></td>
<td>edit</td>
<td>photos.edit</td>
<td>Show the form to edit a photo</td>
</tr>
<tr>
<td>PUT/PATCH</td>
<td><code>/photos/{id}</code></td>
<td>update</td>
<td>photos.update</td>
<td>Update the specified photo</td>
</tr>
<tr>
<td>DELETE</td>
<td><code>/photos/{id}</code></td>
<td>destroy</td>
<td>photos.destroy</td>
<td>Delete the specified photo</td>
</tr>
</tbody>
</table>

# Put vs Post vs Patch