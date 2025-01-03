<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RFID Input Example</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .table-container {
            margin-top: 20px;
        }
    </style>
</head>

<body>
    <div class="container">
        <h1 class="text-center mt-4">RFID Card Data Input</h1>
        <div class="row mt-4">
            <div class="col-md-6">
                <div class="mb-3">
                    <label for="rfidInput" class="form-label">Scan RFID Card:</label>
                    <input type="text" id="rfidInput" class="form-control" placeholder="Scan your RFID card here"
                        autofocus>
                </div>
            </div>
        </div>
        <div class="row table-container">
            <div class="col-md-6">
                <h4>Data Asli</h4>
                <table class="table table-bordered table-striped" id="dataTable">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Name</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Original data rows -->
                        <tr>
                            <td>0005050991</td>
                            <td>Bob Brown</td>
                        </tr>
                        <tr>
                            <td>0006659352</td>
                            <td>John Doe</td>
                        </tr>
                        <tr>
                            <td>0005732781</td>
                            <td>Jane Smith</td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="col-md-6">
                <h4>Temporary Table</h4>
                <table class="table table-bordered table-striped" id="tempTable">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Name</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Temporary data rows -->
                    </tbody>
                </table>
            </div>
        </div>
    </div>
    <script>
        // Temporary list for added data
        const tempData = [];
        const tempTableBody = document.getElementById('tempTable').querySelector('tbody');
        const rfidInput = document.getElementById('rfidInput');

        const mockDatabase = {
            // '112233': 'Alice Johnson',
            '0005050991': 'Bob Brown',
            '0006659352': 'John Doe',
            '0005732781': 'Jane Smith'
        };

        //////////////////////////////// RFID DI IZINKAN SEKALI ///////////////////////////////////////////////////////////////////
        // // Event listener for RFID input on Enter key
        // rfidInput.addEventListener('keypress', (event) => {
        //     if (event.key === 'Enter') { // Detect Enter key
        //         const rfid = rfidInput.value.trim();
        //         if (mockDatabase[rfid]) {
        //             // Add to temporary table if RFID exists in mock database
        //             if (!tempData.includes(rfid)) {
        //                 tempData.push(rfid);
        //                 const row = document.createElement('tr');
        //                 row.innerHTML = `<td>${rfid}</td><td>${mockDatabase[rfid]}</td>`;
        //                 tempTableBody.appendChild(row);
        //             } else {
        //                 alert('RFID already added to temporary table.');
        //             }
        //         } else {
        //             alert('Invalid RFID!');
        //         }
        //         rfidInput.value = ''; // Clear input field
        //         event.preventDefault(); // Prevent form submission
        //     }
        // });

        ///////////////////////////////// INPUT RFID DIBATASI 2 KALI ///////////////////////////////////////////////
        // // Event listener for RFID input on Enter key
        // rfidInput.addEventListener('keypress', (event) => {
        //     if (event.key === 'Enter') { // Detect Enter key
        //         const rfid = rfidInput.value.trim();
        //         if (mockDatabase[rfid]) {
        //             // Count occurrences of RFID in tempData
        //             const rfidCount = tempData.filter(item => item === rfid).length;

        //             if (rfidCount < 2) { // Allow up to two occurrences
        //                 tempData.push(rfid);
        //                 const row = document.createElement('tr');
        //                 row.innerHTML = `<td>${rfid}</td><td>${mockDatabase[rfid]}</td>`;
        //                 tempTableBody.appendChild(row);
        //             } else {
        //                 alert('RFID already added twice to the temporary table.');
        //             }
        //         } else {
        //             alert('Invalid RFID!');
        //         }
        //         rfidInput.value = ''; // Clear input field
        //         event.preventDefault(); // Prevent form submission
        //     }
        // });


        ///////////////////////////////// INPUT RFID TIDAK DIBATASI ///////////////////////////////////////////////
        // Event listener for RFID input on Enter key
        rfidInput.addEventListener('keypress', (event) => {
            if (event.key === 'Enter') { // Detect Enter key
                const rfid = rfidInput.value.trim();
                if (mockDatabase[rfid]) {
                    // Add RFID to the temporary table without restriction
                    tempData.push(rfid);
                    const row = document.createElement('tr');
                    row.innerHTML = `<td>${rfid}</td><td>${mockDatabase[rfid]}</td>`;
                    tempTableBody.appendChild(row);
                } else {
                    alert('Invalid RFID!');
                }
                rfidInput.value = ''; // Clear input field
                event.preventDefault(); // Prevent form submission
            }
        });
    </script>
</body>

</html>
