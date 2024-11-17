# eCitizen-Kenya-API
This Repository offers an insight into eCitizen Payments and how to Integrate eCitizen Payments API to your Website for Payments Checkout Process
<p> We all have interracted with eCitizen in one way or another in our interractions with Government Services eg
<li> Passport Payment</li>
<li> County Services Payments</li>
<li> Renewal of Driving License (More Common)</li>
<br>
But have you ever thought how the payment iframe Generation happens?
</p>
<strong> We shall delve into 3 aspects of the API. </strong>

<ol>
<li>1.Generate Secure Hash </li>
<li>2.Payment Initiation Request</li>
<li>3.Payment Verification Request </li>
</ol>

<h1> Generate Secure Hash </h1>
<p> This is not actually an API but more of a Method that Generates the Secure Hash to be passed when requesting the eCitizen Iframe. This Hash is generated and passed as part of the request to indeed confirm that the request originates from a valid user who is recognized by the eCitizen API Engine on the backend.
</p>

<p>To Generate the Secure Hash You need the <strong>api_client_id</strong>,<strong>ref_no</strong>
<br>
  <strong>api_client_key</strong> - This value is assigned to you by the eCitizen Team and is Unique for Every Client <br>
<strong>api_client_id</strong> - This value is assigned to you by the eCitizen Team and is unique for every Client <br>
<strong>ref_no</strong> - This is a unique value that is generated to identify the Transaction. We can call it a Unique Transaction Ref</p>

<h5> Generating the Secure Hash</h5>
To arrive at the Secure Hash you need to compute a cryptographic hash of a string that contains the api_client_id and the ref_no using the HMAC (Hash-based Message Authentication Code) mechanism with the SHA-256 algorithm.
<code>
public function generateSecureHashEcitizen($api_client_id,$ref_no,$api_client_key){

    $datastring     = $api_client_id.$ref_no;
    //Sign the payload with the api_client_key to arrive at the secure_hash
    $hash           = hash_hmac("sha256",$datastring,$api_client_key'));
    //encode the Secure binary hash with base64
    $secure_hash    = base64_encode($hash);

    return $secure_hash;

}
</code>

The Final Secure Hash looks like this
<code>
MDY5YTM0NDBlZjAwYTExYjQyODE1ZTE2ZTZiNjVjYWViNzRlNjU3ZTNjZDc4ZTRkMzMwOGQyZjQ5ODA2MjU3OA==
</code>




