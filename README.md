# Azure Blob Storage Function

An **Azure Functions** project that provides HTTP endpoints for uploading and deleting files stored in **Azure Blob Storage**.

The project demonstrates how a serverless Azure Function can communicate with Blob Storage to manage files without requiring a traditional web server.

> **Project Status:** Completed

## About the Project

This project was created to explore **serverless computing and cloud storage using Microsoft Azure**.

The application uses **Azure Functions** to expose HTTP endpoints that interact with an Azure Blob Storage container named `products`.

The function supports:

* Uploading files to Blob Storage
* Deleting files from Blob Storage
* Creating the Blob Storage container automatically when required
* Logging function activity
* Handling errors during storage operations

## Architecture

```text
HTTP Client
     │
     │ POST / Upload
     │ DELETE / Delete
     ▼
Azure Functions
     │
     ▼
BlobServiceClient
     │
     ▼
Azure Blob Storage
     │
     ▼
products Container
```

## Features

### Upload to Blob Storage

The `UploadToBlob` function handles HTTP `POST` requests.

The function:

1. Receives a file through the HTTP request body.
2. Retrieves the filename from the `file-name` request header.
3. Connects to the `products` Blob Storage container.
4. Creates the container if it does not already exist.
5. Uploads the file.
6. Allows an existing blob with the same name to be overwritten.
7. Returns a success or error response.

### Delete Blob

The `DeleteBlob` function handles HTTP `DELETE` requests.

The function:

1. Receives a Blob Storage URI through the query string.
2. Extracts the blob filename.
3. Connects to the `products` container.
4. Deletes the specified blob.
5. Includes blob snapshots when deleting.
6. Returns a success or error response.

## Technologies Used

### Cloud

* Microsoft Azure
* Azure Functions
* Azure Blob Storage

### Development

* C#
* .NET
* Azure Storage Blobs SDK

### Tools

* Visual Studio
* Git
* GitHub

## Azure Services

### Azure Functions

Azure Functions provides the serverless execution environment for the application.

The project contains two HTTP-triggered functions:

```text
UploadToBlob
    POST

DeleteBlob
    DELETE
```

### Azure Blob Storage

Blob Storage is used to store files in a container called:

```text
products
```

The application uses `BlobServiceClient` to communicate with the storage account.

## Configuration

The Azure Storage connection string is retrieved through the environment variable:

```text
AzureWebJobsStorage
```

This allows the storage connection information to be provided through the Azure Function configuration rather than being hardcoded into the application.

## API Endpoints

### Upload

```text
POST /api/UploadToBlob
```

The filename is provided through the request header:

```text
file-name: example.jpg
```

The file contents are sent through the request body.

Successful requests return:

```text
Blob 'example.jpg' uploaded successfully.
```

### Delete

```text
DELETE /api/DeleteBlob?blobUri={blobUri}
```

The Blob Storage URI is provided through the query string.

Successful requests return:

```text
Blob 'example.jpg' deleted successfully.
```

## Error Handling

The functions include exception handling and logging.

If an operation fails, the function:

* Logs the error
* Returns an HTTP `500 Internal Server Error`
* Provides a failure response to the client

## Project Structure

```text
BlobST
│
├── BlobStorageFunction.cs
├── Program.cs
├── host.json
├── local.settings.json
└── BlobST.csproj
```

> `local.settings.json` should not be committed to GitHub if it contains storage connection strings or other secrets.

## What I Learned

Through this project, I developed experience with:

* Azure Functions
* Serverless application development
* Azure Blob Storage
* C# cloud development
* HTTP-triggered functions
* Uploading files to cloud storage
* Deleting cloud files programmatically
* Azure Storage SDK
* Environment variables and configuration
* Logging and exception handling
* Git and GitHub

## Cloud Architecture Concepts

This project introduced several important cloud concepts:

* **Serverless computing** through Azure Functions
* **Cloud object storage** through Azure Blob Storage
* **Event/API-driven architecture** through HTTP triggers
* **Managed cloud services**
* **Environment-based configuration**
* **Scalable file storage**

## Future Improvements

Potential improvements include:

* File type validation
* File size restrictions
* Unique blob naming
* Secure authentication and authorization
* Azure Managed Identity instead of connection strings
* Generate SAS URLs for controlled file access
* Integrate the function with an ASP.NET Core MVC application
* Add automated testing
* Add CI/CD with GitHub Actions
* Add Application Insights monitoring

## Author

**Lydia Bizuhen**

Computer Science Student | ASP.NET Core | Azure | Cloud Development

## License

This project was created for educational and portfolio purposes.
