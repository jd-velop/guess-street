# **Use Cases**

## **Actors**

- **Predictors**: those who make predictions to gain credibility and exposure on their separate platforms. Registers with email and password, verifies account, logs in, and creates predictions.
  - IS-A relationship with Authenticated Users.
- **Authenticated Users**: Regular users who have successfully authenticated with the email and own a username and password.
  - IS-A relationship with Regular Users.
- **Regular Users**: non-authenicated members of the community who want to track predictions made by authenticated predictors.
- **Admins**: System maintainers with the highest level of access. Can perform commands that other users cannot, such as banning users, deleting accounts.

## **Use Cases**

- **UC1**: Authenticated Users can make a prediction on a specific asset and become a Predictor.
  - The ability to create predictions is the core function of the platform. Without it, the system does not fulfill its purpose. By allowing authenticated users to create predictions on financial assets, the platform enables them to contribute to the platform and build a prediction history. This directly supports the business requirement of providing a transparent way to create and track predictions over time.
- **UC2**: Predictors can gain quantifiable credibility through successful financial predictions.
  - One of the biggest features of the platform that sets it apart from others is accountability. By measuring accuracy of a prediction against its real market outcome, the system provides a fair way for a predictor to gain credibility. Through this system, predictors are rewarded for accurate predictions rather than speculations, which encourages trust, engagement, and long-term adoption of the platform.
- **UC3**: Regular users can view all predictions made by a specific predictor.
  - Transparency is a core value of the platform. Allowing the full history of a user's predictions to be viewed helps the platform build a reputation-based community. Having a way to view all the predictions of a specific predictor can give a user the context of the predictor’s credibility and base their financial decisions on that information.
- **UC4**: Regular users can view all predictions made for a specific asset.
  - Similar to allowing a user to see all the predictions made from an individual predictor, allowing all the predictions to be made on a single asset leads to a higher level of transparency for the user as well. Having a way to view all predictions made on a single asset can give the user the context of the stability of an asset and base their financial decisions on that information.
- **UC5**: Admins can perform maintenance on technology of the platform to repair, maintain, and expand upon the software.
  - Another core value of this platform is for the users or predictors to not be able to see the backend of the API. Without the abstraction for only Admins to see what parts of the technology need repaired, maintained, or expanded, the users and predictors would get a less-clean, more-jumbled view of the platform and would  be considered a distraction to the aim of the platform itself, which is for predictors to make predictions and users to base their financial decisions on the credibility of the predictor.
- **UC6**: Admins can enforce temporary or permanent bans for misuse of platform 
  - The aim of this platform is to give a space for predictors to make public predictions on assets and for users to see their credibility of these predictors. If a predictor or user is misusing the platform to do things besides what is its aim, Admin can either temporarily or permanently ban individual accounts (either predictors or authenticated users) to make sure the platform is used as intended.
- **UC7**: Authenticated users can follow Predictors.
  - To keep track of predictors that a user has deemed credible enough to track their predictions, those users who have created accounts and logged in can follow those trusted predictors to stay up to date on their predictions. The predictions are shown to the user on their home page. This upholds the ability of a user to track the predictions made by a specific user, which is one of the goals of the platform.
- **UC8**: Authenticated Users can use their account information to gain access to their profile.
  - After creating an account, a user is not expected to use a single device to interact with the platform. Using the information given upon creating an account and becoming an authenticated user, the user can sign into their account to gain access to their profile. This allows them to perform certain actions, such as following predictors. 
- **UC9**: Regular users can create an account to become an Authenticated User.
  - Email verification ensures that the platform only admits real and valid users. This also allows the user to now be able to perform specific actions, such as following predictors, to more easily track credibility, upholding the aim of this platform.
- **UC10**: Authenticated users can turn on notifications for followed Predictors.
  - Similar to the reasoning behind being able to follow predictors, those who a user has deemed credible enough to track their predictions, a user who turns on notifications for a predictor will be automatically notified when that specific predictor makes a new prediction or a prediction outcome has been decided. This will uphold the aim of this platform, which is for users to be able to track the predictions made by specific predictors.
