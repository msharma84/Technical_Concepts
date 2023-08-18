# BLUE-GREEN Deployment

Blue-green deployment is a technique that reduces downtime and risk by running two identical production environments called Blue and Green.
At any time, only one of the environments is live, with the live environment serving all production traffic. For this example, Blue is currently live and Green is idle.

As you prepare a new version of your software, deployment and the final stage of testing takes place in the environment that is not live: in this example, Green. Once you have deployed and fully tested the software in Green, you switch the router so all incoming requests now go to Green instead of Blue. Green is now live, and Blue is idle.

This technique can eliminate downtime due to app deployment. In addition, blue-green deployment reduces risk: if something unexpected happens with your new version on Green, you can immediately roll back to the last version by switching back to Blue.

If your app uses a relational database, blue-green deployment can lead to discrepancies between your Green and Blue databases during an update. To maximize data integrity, configure a single database for backward and forward compatibility.

# CANARY Deployment

Canary deployment is like blue-green, except it’s more risk-averse. Instead of switching from blue to green in one step, you use a phased approach.

With canary deployment, you deploy a new application code in a small part of the production infrastructure. Once the application is signed off for release, only a few users are routed to it. This minimizes any impact.

The main challenge of canary deployment is to devise a way to route some users to the new application. Also, some applications may always need the same group of users for testing, while others may require a different group every time.

Consider a way to route new users by exploring several techniques:

 * Exposing internal users to the canary deployment before allowing external user access;
 * Basing routing on the source IP range;
 * Releasing the application in specific geographic regions;
 * Using an application logic to unlock new features to specific users and groups. This logic is removed when the application goes live for the rest of the users.
