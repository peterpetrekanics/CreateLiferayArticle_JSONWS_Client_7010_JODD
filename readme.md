# CreateLiferayArticle_JSONWS_Client_7010_JODD

This app will create Web Content (Journal) articles, with images on a Liferay 7010 server.

Requirements / steps:

1. Install the fix of LPS-98290  on your portal
2. Make sure that these properties in your portal-ext.properties file allow the uploading of the image that you are planning to upload along with your new web content article:
dl.file.max.size
com.liferay.portal.upload.UploadServletRequestImpl.max.size
com.liferay.portal.upload.LiferayFileItem.threshold.size
You need to set these properties to a higher value than your image file size.
Note: the App now support multiple images as well.
3. Start your portal
4. Once the portal is running, check your portal database for the following values and note them down:
SELECT groupId FROM Your_DB_Name.Group_  where groupKey = 'Guest';
SELECT templateKey FROM Your_DB_Name.DDMTemplate where userName like "Test Test";
SELECT structureKey FROM Your_DB_Name.DDMStructure where userName like "Test Test";
5. Create a new Web Content Article structure: 
- give a name to your structure
- drag and drop the "Image" field to your structure
- click on the "Image" field to display it's properties
rename the Field Label from: "Image" to "image"
6. Create a new Web Content Article template, based on your structure:
the template should only contain this line:
{code}src="${image.getData()}"{code}
7. Place an Asset Publisher portlet to your Welcome page:
within Asset Publisher, click on: Configuration / Display Settings / Display Template:
instead of Abstracts choose: Full Content and click Save.
8. Compile and start the App
Make sure you have the correct values before starting:
groupId, templateKey, structureKey, content.
The content has to be created based on the Portal database (JournalArticle table's "content" column)

9. Visit your Welcome page to see whether the new article appears within Asset Publisher.

Behavior without the fix of LPS-98290 installed:
When checking the created web content, the image doesn't appear.

Behavior with the fix of LPS-98290 installed:
When checking the created web content, the image appears as intended.