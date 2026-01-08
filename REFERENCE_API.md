1. Create Charge 
curl --location 'https://hrms-dev-api-mum.delhivery.com/payouts/api/v1/OFR/charges' \
--header 'Authorization: Bearer xxx' \
--header 'Content-Type: application/json' \
--data '{
    "cycle_start_date": {{epoch_start_date}},
    "cycle_end_date": {{epoch_end_date}},
    "entity_code": {{vendor_code}},
    "entity_type": "VENDOR",
    "sub_type": {{charge_sub_type}},
    "address_state": {{state_of_user}},
    "facility_code": {{facility_code}},
    "operational_type": "Retail",
    "is_gst_registered": true,
    "editable_invoice": {{is_invoice_editable}},
    "payout_category": "DB",
    "type": "SALARY",
    "amount": {{amount_by_user}},
    "tax_amount": 250, // 18 percent of the amount
    "user_type": "OFR",
    "is_last_charge": {{is_invoice_editable}},
    "invoice_id": {{external_charge_id}} + {{randome_number_from_1_to_100}},
    "external_charge_id": {{external_charge_id}},
    "additional_info": {
        "create_invoice": true,
        "group_name": {{random_group_name}},
        "notes": "Urgent processing required",
        "priority": "High",
        "invoice_start_date": {{epoch_start_date}},
        "invoice_end_date": {{epoch_end_date}},
        "external_invoice_id": {{external_charge_id}},
        "invoice_name": {{invoice_name_entered_by_user}}
    },
    "description": "Monthly service",
    "tenant_id": "tenant_001"
}'

Response:
{
    "error_message": null,
    "message": "Charge created successfully",
    "data": {
        "cycle_start_date": 1764583980,
        "cycle_end_date": 1767175980,
        "entity_code": "VENDOR0001139",
        "entity_type": "VENDOR",
        "sub_type": "SERVICE_CHARGE",
        "address_state": "NEW DELHI",
        "facility_code": "INHRAHXW",
        "operational_type": "Retail",
        "is_gst_registered": true,
        "editable_invoice": true,
        "payout_category": "DB",
        "type": "SALARY",
        "amount": 2500.0,
        "tax_amount": 250.0,
        "external_charge_id": "INVOICEDINESHTEST21080",
        "additional_info": {
            "create_invoice": true,
            "group_name": "riya-dinesh-1",
            "notes": "Urgent processing required",
            "priority": "High",
            "invoice_start_date": 1764583980,
            "invoice_end_date": 1767175980,
            "external_invoice_id": "INVOICEDINESHTEST21080",
            "invoice_name": "DINESH- RIYA 3"
        },
        "description": "Monthly service",
        "state": "created",
        "request_type": null,
        "id": "32229551-b2a5-430d-b878-4d2146fbf572",
        "invoice_id": "7e3db0ad-f764-4121-a3e5-bcea8fb1eaa8",
        "user_type": "OFR",
        "created_at": "2026-01-08T12:04:01.936108",
        "updated_at": "2026-01-08T12:04:01.936108",
        "created_by": "SSN027556",
        "updated_by": "SSN027556"
    },
    "attributes": null,
    "traceback": null
}

1.a API to create chagre details:
curl --location 'https://hrms-dev-api-mum.delhivery.com/payouts/api/v1/OFR/charge-details' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer xxx' \
--data '{
    "entity_code": {{vendor_code}},
    "user_type": "OFR",
    "entity_type": "VENDOR",
    "charge_id": {{charge_id}},
    "cycle_start_date": {{epoch_start_date}},
    "cycle_end_date": {{epoch_end_date}},
    "amount": {{amount_by_user}},
    "tax_amount": {{gst_18_percentage}},
    "description": "Storage charges for Riya 2025",
    "additional_info": {
        "center_code": {{facility_code}},
        "facility_code": {{facility_code}},
        "centre_name": "AUTOFC3",
        "facility_name": "AUTOFC3",
        "total_ctc": 2500.0, 
        "operation_type": "Delhivery-Warehouse", 
        "warehouse_location": "New Delhi", 
        "billing_period": "Q1-2024", 
        "square_footage": 5000, 
        "rate_per_sqft": 0.30 
    }
}'



2. Approve Charge
Take charge id from the above api response:
curl --location --globoff --request PUT 'https://hrms-dev-api-mum.delhivery.com/payouts/api/v1/OFR/charges/{{charge_id}}' \
--header 'Authorization: Bearer xxx' \
--header 'Content-Type: application/json' \
--data '{
    "status": {
        "action": "approve",
        "current_state": "created"
    }
}'

Response:
{
    "error_message": null,
    "message": "Charge status updated successfully",
    "data": null,
    "attributes": null,
    "traceback": null
}


3. Fetch all invoices 
curl --location 'https://hrms-dev-api-mum.delhivery.com/payouts/api/v1/OFR/employee/invoices?page=1&view_type=all' \
--header 'Authorization: Bearer xxx' \
--header 'Referer: https://qa-hrms-mum.delhivery.com/' \
--header 'Accept: application/json, text/plain, */*'


Response:
{
    "error_message": null,
    "message": "Employee invoices retrieved successfully for OFR with view_type: all",
    "data": {
        "items": [
            {
                "name": "DINESH- RIYA 3",
                "id": "7e3db0ad-f764-4121-a3e5-bcea8fb1eaa8",
                "invoice_number": null,
                "external_invoice_id": "INVOICEDINESHTEST21080",
                "type": "SALARY",
                "invoice_start_date": 1764583980,
                "invoice_end_date": 1767175980,
                "vendor_operation_state": "NEW DELHI",
                "amount": 2500.0,
                "amount_with_tax": 2950.0,
                "tax": 450.0,
                "user_type": "OFR",
                "operational_type": "Delhivery -Transport",
                "entity_code": "VENDOR0001139",
                "entity_type": "VENDOR",
                "description": "Monthly service",
                "address_state": null,
                "editable_invoice": true,
                "additional_info": {
                    "create_invoice": true,
                    "group_name": "riya-dinesh-1",
                    "notes": "Urgent processing required",
                    "priority": "High",
                    "invoice_start_date": 1764583980,
                    "invoice_end_date": 1767175980,
                    "external_invoice_id": "INVOICEDINESHTEST21080",
                    "invoice_name": "DINESH- RIYA 3",
                    "vendor_name": "New Agency V4",
                    "penalty_amount": 0
                },
                "state": "pending",
                "created_at": "2026-01-08T12:04:01.444975",
                "updated_at": "2026-01-08T12:04:44.904748",
                "created_by": "SSN027556",
                "updated_by": "SSN027556",
                "ui_info": {
                    "status_text": "Pending",
                    "action_on": "N/A"
                },
                "payments": null
            }],
        "total": 1200,
        "page": 1,
        "size": 10,
        "total_pages": 120,
        "has_next": true,
        "has_prev": false
    },
    "attributes": null,
    "traceback": null
}


4. API to upload Invoice by the vendor:
curl --location 'https://hrms-dev-api.delhivery.com/vendor/payouts/api/v1/files/presigned-url' \
--header 'authorization: Bearer {{vendor_token}}' \
--header 'content-type: application/json' \
--header 'origin: https://manpower.delhivery.com' \
--data '{
    "upload_type": "uploaders",
    "module": "invoices",
    "id": {{invoice_id}},
    "content_type": "application/pdf",
    "operation": "put_object"
}'

Response:
{
    "attributes": null,
    "data": {
        "content_type": "application/pdf",
        "expires_in": 3600,
        "headers_for_presigned": {
            "Content-Type": "application/pdf"
        },
        "key": "payouts/invoices/66b64766-ed43-40a0-81cc-aadbe2baf783/20260108_103108_584.pdf",
        "meta_data": {},
        "url": "https://newton-offroll-dev-mum.s3.amazonaws.com/payouts/invoices/66b64766-ed43-40a0-81cc-aadbe2baf783/20260108_103108_584.pdf?......."
    },
    "error_message": null,
    "message": "Presigned URL generated successfully",
    "traceback": null
}

5. API to update sequence number:
curl --location --request PUT 'https://hrms-dev-api.delhivery.com/vendor/payouts/api/v1/OFR/vendor/invoices/{{invoice_id}}' \
--header 'accept: application/json, text/plain, */*' \
--header 'authorization: Bearer xxx' \
--header 'content-type: application/json' \
--header 'origin: https://manpower-dev-ui.pntrzz.com' \
--header 'referer: https://manpower-dev-ui.pntrzz.com/' \
--data '{
    "s3_file_path": {{s3_path}},
    "sequence_number": {{dequence_number}},
    "encrypted_gst_number": {{encrypted_gst_number}},
    "invoice_date": {{invoice_date}},
    "vendor_selected_state":{{vendor_selected_state}}
}'


6. Approve Invoice:
Take invoice id from the invoice api response:
curl --location --globoff --request PUT 'https://hrms-dev-api-mum.delhivery.com/payouts/api/v1/OFR/invoices/{{invoice_id}}' \
--header 'Authorization: Bearer xxx' \
--header 'Content-Type: application/json' \
--data '{
    "status": {
        "action": "approve",
        "current_state": {{state_from_invoice_api_response}}
    }
}'

Response:
{
    "error_message": null,
    "message": "Charge status updated successfully",
    "data": null,
    "attributes": null,
    "traceback": null
}