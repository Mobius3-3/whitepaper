<p align="center">
  <img 
    src="https://res.cloudinary.com/vidsy/image/upload/v1509658596/circle19_viaray.gif" 
    width="300px"
  >
</p>

<h1 align="center">BlockAuth Whitepaper</h1>

<p align="center">
  Whitepaper explaining <a href="https://github.com/blockauth">BlockAuth</a>.
</p>

## Aims

The BlockAuth project aims to:

1. Allow businesses to use the NEO blockchain for **passwordless authentication**.
1. Provide a solution that businesses **outside** of the NEO ecosystem can use **today**.
1. Bring **awareness** to the NEO ecosystem. 
1. Improve the security of web application by moving away from **email/password** based authentication.

## Diagram

![http://res.cloudinary.com/vidsy/image/upload/v1510875557/BlockAuth_Diagram_2_zn6ipd.svg](http://res.cloudinary.com/vidsy/image/upload/v1510875557/BlockAuth_Diagram_2_zn6ipd.svg)

## Technical

TODO

## Limitations

Currently the key used within the `Storage.Put()` operation in the [smart-contract](https://github.com/blockauth/smart-contract) is made up of
two randomly generated [version 4](https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_.28random.29) UUIDs.

```
<random_uuid>.<random_uuid>
```
```
ce8c00c2-4fa5-47de-a07e-1061e62955b0.3b19cfed-9731-4bb4-a5ef-f9fe052bb79e
```

This means that all storage keys are shared between all users invoking the smart contract. Therefore a malicious attacker could carry out an 
extremely large [denial-of-service](https://en.wikipedia.org/wiki/Denial-of-service_attack) attack, that could block users from logging in.

This exploit would not allow the malicious attacker to login as a different user, but simply block other users from completing a login attempt.

This however is extremely unlikely due to the number of combinations a UUID could have. The malicious attacker would have a 50% chance of 
blocking another user after generating 2.71 quintillion UUIDs.

This will be fixed in the future by changing how the storage key is generated. It will become:

```
<random_uuid>.<users_neo_public_address>
```
```
ce8c00c2-4fa5-47de-a07e-1061e62955b0.AS3vAZfkFfvyvgSV5e9hwx3oNnJ3ZQ67ct
```

The second part of the storage key will be the NEO public address of the user that invoked the smart contract. Therefore they will only be able
to affect their own login attempts, as the storage key is always unqiue to their NEO public address.

This was not implemented within [v3.0.0](https://github.com/blockauth/smart-contract/releases/tag/3.0.0) of the smart contract because of a 
limitation in [neo-python](https://github.com/CityOfZion/neo-python). BlockAuth will look to implement the necessary features to be able to 
fix this limitation. 

## Future

BlockAuth will continue to build new innovative products in the future.

### Serverless

Currently a business needs to deploy and maintain a hosted instance of the BlockAuth [server](https://github.com/blockauth/server). This is a
barrier to entry, relatively expensive and needs constant monitoring.

In the future the BlockAuth [server](https://github.com/blockauth/server) can be moved to run within [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html).

The deployment to a lambda function can be automated, and so reduces the barrier to entry for a business wishing to use BlockAuth. Serverless is
far more cost effective than running a dedicated host. Lambda functions can not "go down", and so removes the worry of monitoring.

## Embeddable Login Form

Businesses currently will have to use the BlockAuth [client](https://github.com/blockauth/client) (Javascript library) to implement a BlockAuth solution.

In the future, a business will instead install a single dependency that will act as an embeddable login form for desktop and mobile.

A great example of this product is the [Auth0 Lock](https://auth0.com/lock).

---

<p align="center">
  Check out the BlockAuth <a href="http://demo.blockauth.cc/">Demo</a>.
  <br>
  🔐
</p>
