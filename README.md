# Document Viewer for Microsoft Dynamics 365

A responsive HTML document viewer component for Microsoft Dynamics 365 that displays PDF files and images stored in entity records. Features include zoom, rotation, page navigation, and download functionality.

## Features

- **Multi-format Support**: View PDF files and images (JPG, PNG, GIF)
- **PDF Navigation**: Single page view or continuous scroll mode for multi-page PDFs
- **Interactive Controls**: Zoom in/out, rotate, reset view, and download
- **Responsive Design**: Works on desktop, tablet, and mobile devices
- **High-Quality Rendering**: Enhanced PDF rendering with device pixel ratio support
- **Download Functionality**: Direct file download with proper file extensions

## Setup Instructions

### 1. Prepare Your Dynamics 365 Entity

Ensure your entity has the following fields:
- A **file field** (stores the actual file data)
- The standard **name field** (primary name field that exists on all Dataverse tables)

### 2. Configure the HTML Code

Replace the following placeholders in the HTML file with your actual table and field names:

#### Required Replacements:

| Placeholder | Replace With | Description |
|-------------|--------------|-------------|
| `{table_set_name}` | Your entity set name | Plural form of your entity (e.g., `new_documents`, `contacts`) |
| `{table_name}` | Primary name field | Usually `new_name`, `cr7a1_name`, etc. (with your publisher prefix) |
| `{table_filedata}` | Your file field | API name of the field storing the file data |

#### Example Configuration:

If you have an entity called "Document" with:
- Entity set name: `new_documents`
- Primary name field: `new_name`
- File field: `new_filedata`

Replace:
```javascript
// Original placeholders
var apiUrl = window.location.origin + "/api/data/v9.0/{table_set_name}(" + recordId + ")?$select={table_name},{table_fielddata}";

// Becomes:
var apiUrl = window.location.origin + "/api/data/v9.0/new_documents(" + recordId + ")?$select=new_name,new_filedata";
```

### 3. Complete List of Replacements Needed

Search and replace ALL instances of these placeholders:

1. **`{table_set_name}`** - Replace with your entity set name (appears 3 times)
2. **`{table_name}`** - Replace with your primary name field API name (e.g., `new_name`, `cr7a1_name`) (appears 2 times)  
3. **`{table_filedata}`** - Replace with your file field API name (appears 4 times)

### 4. Deploy to Dynamics 365

1. Save the modified HTML file
2. Upload as a web resource in Dynamics 365:
   - Go to **Settings** > **Customizations** > **Customize the System**
   - Navigate to **Web Resources** > **New**
   - Set **Type** to "Webpage (HTML)"
   - Upload your HTML file
   - **Publish** the customization

### 5. Add to Entity Form

1. Edit your entity form
2. Add an **HTML web resource** control
3. Configure the web resource properties:
   - **Web resource**: Select your uploaded HTML web resource
   - **Name**: Give it a descriptive name (e.g., "DocumentViewer")
   - **Label**: Set the label or hide it as needed
   - **Height**: 600px (or desired height)
4. **Save** and **Publish** the form

## API Field Name Reference

To find your actual field API names:

1. **Via Dynamics 365 UI**:
   - Go to **Settings** > **Customizations** > **Customize the System**
   - Navigate to your entity > **Fields**
   - Look for the **Name** column (this is the API name)

2. **Via Power Platform**:
   - Open [Power Platform admin center](https://admin.powerplatform.microsoft.com)
   - Navigate to your environment > **Data** > **Tables**
   - Find your table and view the **Columns**

3. **Entity Set Name**:
   - Usually the plural form of your entity name
   - Replace spaces with underscores and make lowercase
   - Add publisher prefix (e.g., `new_`, `cr7a1_`)

## Usage

Once deployed, the document viewer will:

1. Automatically detect the current record ID
2. Fetch the file data from the specified fields
3. Display the document with interactive controls
4. Allow users to zoom, rotate, navigate, and download

## Browser Compatibility

- Chrome/Edge (recommended)
- Firefox
- Safari
- Mobile browsers

## File Size Limitations

- Follows Dynamics 365 file attachment limits
- Large PDF files may take longer to render
- Consider file optimization for better performance

## Security Considerations

- Respects Dynamics 365 security roles and permissions
- Users can only view files from records they have access to
- Download functionality maintains security context
