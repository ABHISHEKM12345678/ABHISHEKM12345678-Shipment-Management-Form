<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Shipment Management Form</title>
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
        <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
        <script src="https://login2explore.com/jpdb/resources/js/0.0.3/jpdb-commons.js"></script>
        <script src="js/index.js" defer></script>
    </head>
    <body>
        <div class="container">
            <h2>Shipment Management Form</h2>
            <form id="shipmentForm">
                <div class="form-group">
                    <label>Shipment No:</label>
                    <input type="text" id="shipmentNo" name="shipmentNo" class="form-control" onchange="getShipment()" autofocus>
                </div>

                <div class="form-group">
                    <label>Description:</label>
                    <input type="text" id="description" name="description" class="form-control">
                </div>

                <div class="form-group">
                    <label>Source:</label>
                    <input type="text" id="source" name="source" class="form-control">
                </div>

                <div class="form-group">
                    <label>Destination:</label>
                    <input type="text" id="destination" name="destination" class="form-control">
                </div>

                <div class="form-group">
                    <label>Shipping Date:</label>
                    <input type="date" id="shippingDate" name="shippingDate" class="form-control">
                </div>

                <div class="form-group">
                    <label>Expected Delivery Date:</label>
                    <input type="date" id="expectedDeliveryDate" name="expectedDeliveryDate" class="form-control">
                </div>

                <div class="form-group text-center">
                    <button type="button" id="save" class="btn btn-lg btn-primary" disabled onclick="saveData()">Save</button>
                    <button type="button" id="update" class="btn btn-lg btn-primary" disabled onclick="updateData()">Update</button>
                    <button type="button" id="reset" class="btn btn-lg btn-primary" disabled onclick="resetForm()">Reset</button>
                </div>
            </form>
        </div>

        <script>
            var baseUrl = "http://api.login2explore.com:5577";
            var dbName = "DeliveryDB";
            var rel = "SHIPMENT-TABLE";
            var userCreds = "90934718|-31949208594406555|90956260";

            function validateAndGetFormData() {
                var shipmentNo = $("#shipmentNo").val();
                var description = $("#description").val();
                var source = $("#source").val();
                var destination = $("#destination").val();
                var shippingDate = $("#shippingDate").val();
                var expectedDeliveryDate = $("#expectedDeliveryDate").val();

                if (shipmentNo === "" || description === "" || source === "" || destination === "" || shippingDate === "" || expectedDeliveryDate === "") {
                    alert("All fields must be filled.");
                    return "";
                }

                var jsonStrObj = {
                    shipmentNo: shipmentNo,
                    description: description,
                    source: source,
                    destination: destination,
                    shippingDate: shippingDate,
                    expectedDeliveryDate: expectedDeliveryDate
                };

                return JSON.stringify(jsonStrObj);
            }

            function saveData() {
                var jsonStr = validateAndGetFormData();
                if (jsonStr === "")
                    return;

                var putReqStr = createPUTRequest(userCreds, jsonStr, dbName, rel);
                jQuery.ajaxSetup({async: false});
                var resJsonObj = executeCommandAtGivenBaseUrl(putReqStr, baseUrl, "/api/iml");
                jQuery.ajaxSetup({async: true});
                resetForm();
                $("#shipmentNo").focus();
            }

            function resetForm() {
                $("#shipmentNo").val("");
                $("#description").val("");
                $("#source").val("");
                $("#destination").val("");
                $("#shippingDate").val("");
                $("#expectedDeliveryDate").val("");

                $("#save").prop("disabled", true);
                $("#update").prop("disabled", true);
                $("#reset").prop("disabled", true);

                $("#shipmentNo").focus();
            }

            function updateData() {
                var jsonStr = validateAndGetFormData();
                if (jsonStr === "")
                    return;

                var updateRequest = createUPDATERecordRequest(userCreds, jsonStr, dbName, rel, localStorage.getItem("recno"));
                jQuery.ajaxSetup({async: false});
                var resJsonObj = executeCommandAtGivenBaseUrl(updateRequest, baseUrl, "/api/iml");
                jQuery.ajaxSetup({async: true});

                resetForm();
            }

            function getShipment() {
                var shipmentNoJsonObj = getShipmentNoAsJsonObj();
                var getRequest = createGET_BY_KEYRequest(userCreds, dbName, rel, shipmentNoJsonObj);

                jQuery.ajaxSetup({async: false});
                var resJsonObj = executeCommandAtGivenBaseUrl(getRequest, baseUrl, "/api/irl");
                jQuery.ajaxSetup({async: true});

                if (resJsonObj.status === 400) {
                    $("#save").prop("disabled", false);
                    $("#reset").prop("disabled", false);
                    $("#description").focus();
                } else if (resJsonObj.status === 200) {
                    $("#shipmentNo").prop("disabled", true);
                    fillData(resJsonObj);
                    $("#update").prop("disabled", false);
                    $("#reset").prop("disabled", false);
                    $("#description").focus();
                }
            }

            function getShipmentNoAsJsonObj() {
                var shipmentNo = $('#shipmentNo').val();
                var jsonStr = {
                    shipmentNo: shipmentNo
                };
                return JSON.stringify(jsonStr);
            }

            function fillData(jsonObj) {
                saveRecNo2ls(jsonObj);
                var record = JSON.parse(jsonObj.data).record;
                $("#description").val(record.description);
                $("#source").val(record.source);
                $("#destination").val(record.destination);
                $("#shippingDate").val(record.shippingDate);
                $("#expectedDeliveryDate").val(record.expectedDeliveryDate);
            }

            function saveRecNo2ls(jsonObj) {
                var lvdata = JSON.parse(jsonObj.data);
                localStorage.setItem("recno", lvdata.rec_no);
            }
        </script>
    </body>
</html>
