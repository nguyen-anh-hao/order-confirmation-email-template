# Order Confirmation Email Template

This is an HTML template for the order confirmation email of the Design ITUS club during the back-to-school sales event for the academic year 2024 - 2025.

## Overview

The template provides a structured layout to display order details, including customer information, product details, and total order value. It is designed to be responsive and supports dark mode for improved readability.

## Features

- **Responsive Design**: Adapts to various screen sizes for mobile and desktop views.
- **Dark Mode Support**: Automatically adjusts styles based on the user's system preferences.
- **Customizable Fields**: Placeholders for dynamic content such as customer name, order number, product details, and payment status.

## HTML Structure

1. **Head Section**:
   - Contains metadata and styles for the document.
   - Responsive design and dark mode styles defined within the `<style>` tag.

2. **Body Section**:
   - The email is structured within a central table for better alignment and presentation.
   - A header section with the club's logo and order confirmation title.
   - A content section that includes a personalized greeting, order details, and contact information.
   - A footer section with club information.

## Placeholder Variables

- `{{order_number}}`: The unique order number for the transaction.
- `{{customer_name}}`: The name of the customer.
- `{{product_name}}`: The name of the product ordered.
- `{{quantity}}`: The quantity of the product ordered.
- `{{order_total}}`: The total amount of the order in VND.
- `{{phone_number}}`: The contact number of the customer.
- `{{delivery_method}}`: The method of delivery chosen by the customer.
- `{{payment_status}}`: The status of the payment.

## Usage

To use this template, you can integrate it with Google Sheets and Google Apps Script for an automated mail merge process. Here’s how to do it:

1. **Set Up Google Sheet**:
   - Create a Google Sheet with columns for each placeholder variable (e.g., order_number, customer_name, product_name, quantity, order_total, phone_number, delivery_method, payment_status, Recipient and Email Sent).

   - Here’s a sample table that illustrates how to set up your Google Sheet:
        | order_number | customer_name | product_name| quantity | order_total | phone_number | delivery_method | payment_status | Recipient | Email Sent |
        |--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|
        | 091401 | Nguyễn Anh Hào | Dây đeo IT<br>Dây đeo FIT<br>Pad chuột IT | 1<br>1<br>1 | 112.500 | 0368377883 | Nhận hàng ngày Khai giảng | Thanh toán thành công! | anhhao012004@gmail.com | |

2. **Add the Script**:
   - Open the Google Sheet and go to **Extensions > Apps Script**.
   - Copy and paste the provided Apps Script code into the script editor.
   - To learn more about using Google Apps Script and mail merge, refer to the documentation: [Google Apps Script Mail Merge Documentation](https://developers.google.com/apps-script/samples/automations/mail-merge)

3. **Modify the Script**:
   - Update the `RECIPIENT_COL` and `EMAIL_SENT_COL` constants to match the column names in your sheet for email addresses and email sent status.
   - **Important**: Modify the `fillInTemplateFromObject_` function in the script to ensure it handles your HTML correctly.

   Here’s the modified function:

   ```javascript
    function fillInTemplateFromObject_(template, data) {
        let template_string = template_string.replace(/{{[^{}]+}}/g, key => {
            let value = data[key.replace(/[{}]+/g, "")] || "";

            // Handle line breaks for HTML
            value = value.replace(/(\r\n|\n|\r)/g, '<br>'); // Convert new lines to HTML line breaks

            return escapeData_(value);
        });

        return JSON.parse(template_string);
    }

4. **Create a Draft Email**:
   - In your Gmail account, create a draft email that uses this HTML template as the body. Ensure the subject line matches the one you will use in the script.

5. **Run the Script**:
   - Reload your Google Sheet. You should see a new menu item called **Mail Merge**.
   - Click on **Mail Merge > Send Emails**. You’ll be prompted to enter the subject line for your email draft.
   - The script will send personalized emails based on the data in your sheet and update the "Email Sent" column with the date when the email was sent.