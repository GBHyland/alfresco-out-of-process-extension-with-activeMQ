## ACS Event Model - JSON Schema
For a detailed view of the event content refer to Repo [Event JSON schema](https://github.com/Alfresco/acs-event-model/blob/master/src/main/resources/json-schema).

### Node created event example
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.node.Created",
      "id": "97c1b36c-c569-4c66-8a31-7a8d0b6b804a",
      "source": "/f6d21231-618e-4f12-a920-e498660c5b9d",
      "time": "2020-04-27T12:37:03.560134+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/nodeCreated",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "cb645043-e7d2-4e51-b61d-e6d01582cbab",
         "resource": {
            "id": "7491120a-e2cb-478f-8599-ebf057cc0c7c",
            "name": "testFile.txt",
            "nodeType": "cm:content",
            "primaryAssocQName": "cm:testFile.txt",
            "secondaryParents": [],
            "isFolder": false,
            "isFile": true,
            "createdByUser": {
            "id": "john.doe",
            "displayName": "John Doe"
            },
            "createdAt": "2020-04-27T12:37:03.555624+01:00",
            "modifiedByUser": {
            "id": "jane.doe",
            "displayName": "Jane Doe"
            },
            "modifiedAt": "2020-04-27T12:37:03.557956+01:00",
            "content": {
            "mimeType": "text/plain",
            "sizeInBytes": 16,
            "encoding": "UTF-8"
            },
            "primaryHierarchy": [
            "521aac1c-20eb-444b-a137-2da3d35ee1a8",
            "2641bbe1-39ff-44dc-b47f-736552ad46cc"
            ],
            "properties": {
            "cm:title": "test title"
            },
            "aspectNames": [
            "cm:titled",
            "cm:auditable"
            ]
         }
      }
   }
```
*  The property ```type``` of **org.alfresco.event.node.Created** indicates that this is a node created event.
* The ```data.resource``` object holds properties specific to the node content:
   * The ```createdAt``` and ```displayName``` indicates when the node was created and by whom.
   * The ```primaryHierarchy``` property is an array of parent nodes leading up to the top node in this repo store.
   * The ```properties``` object holds metadata (cm) specific to the file, such as name and other data that may be assigned.

### Node updated event example (node moved)
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.node.Updated",
      "id": "35378a74-e572-4e6c-8107-5418ed28473b",
      "source": "/8a49c5b4-d9aa-4c1d-9dd6-d57d2e8541a7",
      "time": "2020-05-15T11:27:45.266278+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/nodeUpdated",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "5ad32965-fd7d-480f-800d-90821c9d9e0b",
         "resource": {
            "id": "5acc515e-b08f-4898-b53f-ab587bae97d4",
            "primaryHierarchy": [
            "80272be0-0439-4de2-8ff3-a5f4cddc624f",
            "d88a0730-8616-474b-bf92-b56ff975f5c5",
            "cf9da5a5-3c82-47a1-adb6-366352ffd822"
            ],
            "name": "book.jpeg",
            "nodeType": "cm:content",
            "primaryAssocQName": "cm:book.jpeg",
            "secondaryParents": [],
            "createdByUser": {
            "id": "admin",
            "displayName": "Administrator"
            },
            "createdAt": "2020-05-14T15:02:36.684+01:00",
            "modifiedByUser": {
            "id": "admin",
            "displayName": "Administrator"
            },
            "modifiedAt": "2020-05-15T11:27:45.146+01:00",
            "content": {
            "mimeType": "image/jpeg",
            "sizeInBytes": 6210,
            "encoding": "UTF-8"
            },
            "properties": {
            "cm:autoVersion": true,
            "cm:versionType": "MAJOR",
            "cm:versionLabel": "1.0",
            "cm:autoVersionOnUpdateProps": false,
            "exif:pixelXDimension": 195,
            "cm:lastThumbnailModification": [
               "doclib:1589464959119",
               "imgpreview:1589464965398"
            ],
            "exif:pixelYDimension": 130,
            "cm:initialVersion": true
            },
            "aspectNames": [
            "exif:exif",
            "cm:versionable",
            "cm:author",
            "sys:localized",
            "cm:thumbnailModification",
            "sys:referenceable",
            "cm:titled",
            "sys:cascadeUpdate",
            "rn:renditioned",
            "cm:auditable"
            ],
            "isFolder": false,
            "isFile": true
         },
         "resourceBefore": {
            "primaryHierarchy": [
            "fb78e935-5239-4035-b997-65c7cefaa633",
            "d88a0730-8616-474b-bf92-b56ff975f5c5",
            "cf9da5a5-3c82-47a1-adb6-366352ffd822"
            ]
         }
      }
   }
```
*  The property ```type``` of **org.alfresco.event.node.Updated** indicates that this is a node updated event, meaning the node was edited in some form.
* The ```resourceBefore``` property shows a **primaryHierarchy** array indicating that this node was moved. Additionally, you can compare the **primaryHierarchy** array ID's (in the ```resourceBefore``` object) to the **primaryHierarchy** in the ```data.resource``` object and notice that the parent node's IDs are different in some way, further indicating that the file was moved to a different physical location within the repository.

### Node updated event example (content changed)
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.node.Updated",
      "id": "d1b290e3-fa20-4aaa-b81a-04cfc11ef068",
      "source": "/8a49c5b4-d9aa-4c1d-9dd6-d57d2e8541a7",
      "time": "2020-05-15T14:55:46.326144+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/nodeUpdated",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "1870deed-9a41-4a83-a592-1d28beb0f8bf",
         "resource": {
            "id": "3b827125-987e-4ee4-aad6-1e2a0cc3cb5f",
            "primaryHierarchy": [
            "fb78e935-5239-4035-b997-65c7cefaa633",
            "d88a0730-8616-474b-bf92-b56ff975f5c5",
            "cf9da5a5-3c82-47a1-adb6-366352ffd822"
            ],
            "name": "repo_5129.txt",
            "nodeType": "cm:content",
            "primaryAssocQName": "cm:repo_5129.txt",
            "secondaryParents": [],
            "createdByUser": {
            "id": "admin",
            "displayName": "Administrator"
            },
            "createdAt": "2020-05-15T14:50:51.508+01:00",
            "modifiedByUser": {
            "id": "admin",
            "displayName": "Administrator"
            },
            "modifiedAt": "2020-05-15T14:55:46.271+01:00",
            "content": {
            "mimeType": "text/plain",
            "sizeInBytes": 8,
            "encoding": "UTF-8"
            },
            "properties": {
            "app:editInline": true,
            "cm:lastThumbnailModification": [
               "pdf:1589550869589"
            ]
            },
            "aspectNames": [
            "app:inlineeditable",
            "sys:localized",
            "cm:thumbnailModification",
            "sys:referenceable",
            "cm:titled",
            "rn:renditioned",
            "cm:auditable"
            ],
            "isFolder": false,
            "isFile": true
         },
         "resourceBefore": {
            "modifiedAt": "2020-05-15T14:54:29.593+01:00",
            "content": {
            "mimeType": "text/plain",
            "sizeInBytes": 8,
            "encoding": "UTF-8"
            }
         }
      }
   }
```
*  The property ```type``` of **org.alfresco.event.node.Updated** indicates that this is a node updated event, meaning the node was edited in some form.
* The ```resourceBefore``` object shows a **modifiedAt** property, showing when the file was modified and a **content** object which shows little info regarding the details of the edit, however we are able to see that the content of the file was edited in some way.

### Node updated event example (content added)
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.node.Updated",
      "id": "d1b290e3-fa20-4aaa-b81a-04cfc11ef068",
      "source": "/8a49c5b4-d9aa-4c1d-9dd6-d57d2e8541a7",
      "time": "2020-05-15T14:55:46.326144+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/nodeUpdated",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "1870deed-9a41-4a83-a592-1d28beb0f8bf",
         "resource": {
            "@type":"NodeResource",
            "id": "3b827125-987e-4ee4-aad6-1e2a0cc3cb5f",
            "primaryHierarchy": [
            "fb78e935-5239-4035-b997-65c7cefaa633",
            "d88a0730-8616-474b-bf92-b56ff975f5c5",
            "cf9da5a5-3c82-47a1-adb6-366352ffd822"
            ],
            "name": "repo_5129.txt",
            "nodeType": "cm:content",
            "primaryAssocQName": "cm:repo_5129.txt",
            "secondaryParents": [],
            "createdByUser": {
            "id": "admin",
            "displayName": "Administrator"
            },
            "createdAt": "2020-05-15T14:50:51.508+01:00",
            "modifiedByUser": {
            "id": "admin",
            "displayName": "Administrator"
            },
            "modifiedAt": "2020-05-15T14:55:46.271+01:00",
            "content": {
            "mimeType": "text/plain",
            "sizeInBytes": 8,
            "encoding": "UTF-8"
            },
            "properties": {
            "app:editInline": true,
            "cm:lastThumbnailModification": [
               "pdf:1589550869589"
            ]
            },
            "aspectNames": [
            "app:inlineeditable",
            "sys:localized",
            "cm:thumbnailModification",
            "sys:referenceable",
            "cm:titled",
            "rn:renditioned",
            "cm:auditable"
            ],
            "isFolder": false,
            "isFile": true
         },
         "resourceBefore": {
            "@type":"NodeResource",
            "modifiedAt": "2020-05-15T14:54:29.593+01:00",
            "content": {}
         }
      }
   }
```
*  The property ```type``` of **org.alfresco.event.node.Updated** indicates that this is a node updated event, meaning the node was edited in some form.
* The ```resourceBefore``` object shows a **modifiedAt** property, showing when the file was modified. Note that the **resourceBefore** object's properties are different showing **@type** and the **content** object is empty...

### Node updated event example (node type changed)
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.node.Updated",
      "id": "6449e825-5f0d-40b9-904d-4371d717b1d8",
      "source": "/f52eada4-0673-4dd7-8df6-9838ac911a46",
      "time": "2020-05-15T14:10:58.717856+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/nodeUpdated",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "6eef795f-6c9f-46dd-93c2-b248caec8171",
         "resource": {
            "id": "9a6e488b-49a3-41ef-8032-82a2afbd153e",
            "primaryHierarchy": [
            "3244959b-f3a8-4bb9-82f5-d16300148bb8",
            "9e5dd366-1d55-4b84-a8e5-54721d1e3748",
            "190d8f46-13a1-443b-8d16-7e3c9f52cfc7"
            ],
            "name": "testFile.txt",
            "nodeType": "smf:smartFolderTemplate",
            "primaryAssocQName": "cm:testFile.txt",
            "secondaryParents": [],
            "createdByUser": {
            "id": "john.doe",
            "displayName": "John Doe"
            },
            "createdAt": "2020-05-15T14:10:47.314+01:00",
            "modifiedByUser": {
            "id": "john.doe",
            "displayName": "John Doe"
            },
            "modifiedAt": "2020-05-15T14:10:58.696+01:00",
            "content": {
            "mimeType": "text/plain",
            "sizeInBytes": 8,
            "encoding": "UTF-8"
            },
            "properties": {
            "app:editInline": true,
            "cm:lastThumbnailModification": [
               "pdf:1589548249020"
            ]
            },
            "aspectNames": [
            "app:inlineeditable",
            "sys:localized",
            "cm:thumbnailModification",
            "sys:referenceable",
            "cm:titled",
            "rn:renditioned",
            "cm:auditable"
            ],
            "isFile": true,
            "isFolder": false
         },
         "resourceBefore": {
            "nodeType": "cm:content"
         }
      }
   }
```
*  The property ```type``` of **org.alfresco.event.node.Updated** indicates that this is a node updated event, meaning the node was edited in some form.
* The ```resourceBefore``` object shows a property of **nodeType** where the value (_cm:content_) is different than the **nodeType** in the main object (_smf:smartFolderTemplate_). This indicates that the object's type changed from being a smartfolder template to a content type.

### Node updated event example (property added)
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.node.Updated",
      "id": "6449e825-5f0d-40b9-904d-4371d717b1d8",
      "source": "/f52eada4-0673-4dd7-8df6-9838ac911a46",
      "time": "2020-05-15T14:10:58.717856+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/nodeUpdated",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "6eef795f-6c9f-46dd-93c2-b248caec8171",
         "resource": {
            "@type":"NodeResource",
            "id": "9a6e488b-49a3-41ef-8032-82a2afbd153e",
            "primaryHierarchy": [
            "3244959b-f3a8-4bb9-82f5-d16300148bb8",
            "9e5dd366-1d55-4b84-a8e5-54721d1e3748",
            "190d8f46-13a1-443b-8d16-7e3c9f52cfc7"
            ],
            "name": "testFile.txt",
            "nodeType": "smf:smartFolderTemplate",
            "primaryAssocQName": "cm:testFile.txt",
            "secondaryParents": [],
            "createdByUser": {
            "id": "john.doe",
            "displayName": "John Doe"
            },
            "createdAt": "2020-05-15T14:10:47.314+01:00",
            "modifiedByUser": {
            "id": "john.doe",
            "displayName": "John Doe"
            },
            "modifiedAt": "2020-05-15T14:10:58.696+01:00",
            "content": {
            "mimeType": "text/plain",
            "sizeInBytes": 8,
            "encoding": "UTF-8"
            },
            "properties": {
            "app:editInline": true,
            "cm:lastThumbnailModification": [
               "pdf:1589548249020"
            ],
            "cm:title": "Test file1"
            },
            "aspectNames": [
            "app:inlineeditable",
            "sys:localized",
            "cm:thumbnailModification",
            "sys:referenceable",
            "cm:titled",
            "rn:renditioned",
            "cm:auditable"
            ],
            "isFile": true,
            "isFolder": false
         },
         "resourceBefore": {
            "@type":"NodeResource",
            "modifiedAt":"2020-05-12T15:13:10.889+01:00",
            "properties": {
            "cm:title": null
            }
         }
      }
   }
```
*  The property ```type``` of **org.alfresco.event.node.Updated** indicates that this is a node updated event, meaning the node was edited in some form.
* The ```resourceBefore``` object shows a property of **@type** of nodeResource. It also contains a ```properties``` object with the **cm:title** property set to _null_. Compare the ```resourceBefore.properties.cm:title``` value to the ```data.properties.cm:title``` to note the difference. Before, the file contained a _null_ title, and now it contains a title of "Test file1", indicating that the title of the document was changed.

### Node updated event example (property updated)
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.node.Updated",
      "id": "6449e825-5f0d-40b9-904d-4371d717b1d8",
      "source": "/f52eada4-0673-4dd7-8df6-9838ac911a46",
      "time": "2020-05-15T14:10:58.717856+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/nodeUpdated",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "6eef795f-6c9f-46dd-93c2-b248caec8171",
         "resource": {
            "@type":"NodeResource",
            "id": "9a6e488b-49a3-41ef-8032-82a2afbd153e",
            "primaryHierarchy": [
               "3244959b-f3a8-4bb9-82f5-d16300148bb8",
               "9e5dd366-1d55-4b84-a8e5-54721d1e3748",
               "190d8f46-13a1-443b-8d16-7e3c9f52cfc7"
            ],
            "name": "testFile.txt",
            "nodeType": "smf:smartFolderTemplate",
            "primaryAssocQName": "cm:testFile.txt",
            "secondaryParents": [],
            "createdByUser": {
               "id": "john.doe",
               "displayName": "John Doe"
            },
            "createdAt": "2020-05-15T14:10:47.314+01:00",
            "modifiedByUser": {
               "id": "john.doe",
               "displayName": "John Doe"
            },
            "modifiedAt": "2020-05-15T14:10:58.696+01:00",
            "content": {
               "mimeType": "text/plain",
               "sizeInBytes": 8,
               "encoding": "UTF-8"
            },
            "properties": {
               "app:editInline": true,
               "cm:lastThumbnailModification": [
                  "pdf:1589548249020"
               ],
               "cm:title": "Test file2"
            },
            "aspectNames": [
               "app:inlineeditable",
               "sys:localized",
               "cm:thumbnailModification",
               "sys:referenceable",
               "cm:titled",
               "rn:renditioned",
               "cm:auditable"
            ],
            "isFile": true,
            "isFolder": false
         },
         "resourceBefore": {
            "@type":"NodeResource",
            "modifiedAt":"2020-05-14T15:13:10.889+01:00",
            "properties": {
            "cm:title": "Test file1"
            }
         }
      }
   }
```
*  The property ```type``` of **org.alfresco.event.node.Updated** indicates that this is a node updated event, meaning the node was edited in some form.
* The ```resourceBefore.properties``` object shows a property of **cm:title** with a value of "Test file1". Compare that to the ```data.resource.properties.cm:title``` value of "Test file2" to see that this file name was changed.

### Node updated event example (added secondary parent)
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.node.Updated",
      "id": "37de61ba-72c9-4f8e-8f76-19e934c5cacf",
      "source": "/bdf761f0-4190-44e8-853e-37729eec41a7",
      "time": "2023-09-22T16:01:06.95Z",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/nodeUpdated",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "f1a65c60-3b5d-4774-a858-8d7bff036c8a",
         "resource": {
            "@type": "NodeResource",
            "id": "a070d618-cf99-4413-a17d-c9a6d8d2a5a0",
            "primaryHierarchy": [
               "083cd638-79c1-4487-8804-470b45739127",
               "ada3404d-7f62-4ef1-842b-a21b49cefca7",
               "64b691f5-be1c-47e8-ab12-55feffdfc05a",
               "24741732-c8c7-4ffb-9978-432a755768d4",
               "d4bbdf7a-6ced-4fab-ad14-d293b9949d4d"
            ],
            "name": "folderA",
            "nodeType": "cm:folder",
            "createdByUser": {
               "id": "User-EQmyoOlvHPYYHsk",
               "displayName": "FN-User-EQmyoOlvHPYYHsk LN-User-EQmyoOlvHPYYHsk"
            },
            "createdAt": "2023-09-22T15:31:44.687Z",
            "modifiedByUser": {
               "id": "User-EQmyoOlvHPYYHsk",
               "displayName": "FN-User-EQmyoOlvHPYYHsk LN-User-EQmyoOlvHPYYHsk"
            },
            "modifiedAt": "2023-09-22T16:00:05.785Z",
            "properties": {},
            "aspectNames": [
               "cm:auditable"
            ],
            "primaryAssocQName": "cm:folderA",
            "secondaryParents": [
               "c74a32d1-04c2-4010-af29-968409a93640",
               "1adff44b-a9b8-403f-b053-69c36285d4b2"
            ],
            "isFile": false,
            "isFolder": true
         },
         "resourceBefore": {
            "@type": "NodeResource",
            "modifiedAt": "2023-09-22T15:59:58.945Z",
            "secondaryParents": [
               "c74a32d1-04c2-4010-af29-968409a93640"
            ]
         }
      }
   }
```
*  The property ```type``` of **org.alfresco.event.node.Updated** indicates that this is a node updated event, meaning the node was edited in some form.
* The ```resourceBefore.secondaryParents``` array shows a single node ID. Compare that to the ```data.resource.secondaryParents``` array whch shows that there are two node ID's, indicating that a new secondary parent was added to this node.

### File deleted event example
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.node.Deleted",
      "id": "54d95573-1e08-4ed3-946e-123704198c13",
      "source": "/f52eada4-0673-4dd7-8df6-9838ac911a46",
      "time": "2020-05-15T17:19:18.745537+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/nodeDeleted",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "db22f279-bc46-4f1e-b616-fd94c4f813fc",
         "resource": {
            "id": "9e42c4db-765f-4fa0-9afe-8e87b1b419c5",
            "primaryHierarchy": [
               "3244959b-f3a8-4bb9-82f5-d16300148bb8",
               "9e5dd366-1d55-4b84-a8e5-54721d1e3748",
               "190d8f46-13a1-443b-8d16-7e3c9f52cfc7"
            ],
            "name": "testFile.txt",
            "nodeType": "cm:content",
            "primaryAssocQName": "cm:testFile.txt",
            "secondaryParents": [],
            "createdByUser": {
               "id": "john.doe",
               "displayName": "John Doe"
            },
            "createdAt": "2020-05-14T16:57:31.079+01:00",
            "modifiedByUser": {
               "id": "john.doe",
               "displayName": "John Doe"
            },
            "modifiedAt": "2020-05-15T17:03:04.018+01:00",
            "content": {
               "mimeType": "text/plain",
               "sizeInBytes": 16,
               "encoding": "UTF-8"
            },
            "properties": {
               "cm:title": "A different title",
               "app:editInline": true,
               "cm:lastThumbnailModification": [
                  "pdf:1589497052565"
               ]
            },
            "aspectNames": [
               "app:inlineeditable",
               "cm:author",
               "sys:localized",
               "sys:pendingDelete",
               "cm:thumbnailModification",
               "sys:referenceable",
               "cm:titled",
               "rn:renditioned",
               "cm:auditable",
               "cm:taggable"
            ],
            "isFile": true,
            "isFolder": false
         }
      }
   }
```
* The property ```type``` of **org.alfresco.event.node.Deleted** indicates that this node has been deleted.
* The rest of the information is just the latest values of the node prior to deletion.

### Secondary child association created event example
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.assoc.child.Created",
      "id": "6aa2c078-2317-46be-aaff-50df901a5270",
      "source": "/f4fadb99-b29b-453d-b23b-9c33bf22f8eb",
      "time": "2020-06-08T12:33:33.208424+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/childAssocCreated",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "5f63c476-3dc8-4253-b807-31d7cdc4f0cc",
         "resource": {
            "@type": "ChildAssociationResource",
            "assocType": "cm:contains",
            "assocQName": "cm:12323-2341-222-3431-de3360d6e66g",
            "parent": {
               "id": "f47613d7-78b8-43b7-bc07-cb2260d6a66f"
            },
            "child": {
               "id": "9c10d828-eef3-4dfe-a64c-0f903c6de7c6"
            }
         }
      }
   }
```
* Notice that the ```type``` property value is **org.alfresco.event.assoc.child.Created** which indicates that this message regards a node that was created as a associated child of another node.
* ??? ^ Is that correct?

### Secondary child association deleted event example
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.assoc.child.Deleted",
      "id": "2ced8815-748a-48e3-a9ba-93ffb767bc78",
      "source": "/f4fadb99-b29b-453d-b23b-9c33bf22f8eb",
      "time": "2020-06-08T12:36:51.781289+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/childAssocDeleted",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "7e5526fc-8402-4f1f-9560-f997c7fc55d9",
         "resource": {
            "@type": "ChildAssociationResource",
            "assocType": "cm:contains",
            "assocQName": "cm:12323-2341-222-3431-de3360d6e66g",
            "parent": {
               "id": "f47613d7-78b8-43b7-bc07-cb2260d6a66f"
            },
            "child": {
               "id": "9c10d828-eef3-4dfe-a64c-0f903c6de7c6"
            }
         }
      }
   }
```
* Notice that the ```type``` property value is **org.alfresco.event.assoc.child.Deleted** which indicates that this message regards an associated child node that was deleted.
* ??? ^ Is that correct?

### Peer association created event example
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.assoc.peer.Created",
      "id": "081cb242-12d3-46b5-a87c-9358d68e1e27",
      "source": "/f4fadb99-b29b-453d-b23b-9c33bf22f8eb",
      "time": "2020-06-08T12:37:45.902469+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/peerAssocCreated",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "7479d8e5-93d0-48bd-924a-af422ce3fd0a",
         "resource": {
            "@type": "PeerAssociationResource",
            "assocType": "cm:original",
            "source": {
               "id": "c9e55962-cbea-49c0-823b-b83f60bd3f36"
            },
            "target": {
               "id": "9c10d828-eef3-4dfe-a64c-0f903c6de7c6"
            }
         }
      }
   }
```
* Notice that the ```type``` property value is **org.alfresco.event.assoc.peer.Created** which indicates that this message regards an that was created as associated peer node of another node.
* ??? Is this correct ^?
* Note that the two node(s) associated can be identified by looking at the ```data.resource.source``` and ```data.resource.target``` "id" attributes.

### Peer association deleted event example
```
   {
      "specversion": "1.0",
      "type": "org.alfresco.event.assoc.peer.Deleted",
      "id": "98bdd9b6-4be2-4902-8c85-c7eedd498a67",
      "source": "/f4fadb99-b29b-453d-b23b-9c33bf22f8eb",
      "time": "2020-06-08T12:38:41.103607+01:00",
      "dataschema": "https://api.alfresco.com/schema/event/repo/v1/peerAssocDeleted",
      "datacontenttype": "application/json",
      "data": {
         "eventGroupId": "bc5a2d21-a5d1-4721-aee9-0eb8ee9cb75e",
         "resource": {
            "@type": "PeerAssociationResource",
            "assocType": "cm:original",
            "source": {
               "id": "c9e55962-cbea-49c0-823b-b83f60bd3f36"
            },
            "target": {
               "id": "9c10d828-eef3-4dfe-a64c-0f903c6de7c6"
            }
         }
      }
      }
```
* Notice that the ```type``` property value is **org.alfresco.event.assoc.peer.Deleted** which indicates that this message regards an associated peer node that was deleted.
* ??? Is this correct ^?
* Note that the two node(s) associated can be identified by looking at the ```data.resource.source``` and ```data.resource.target``` "id" attributes.

