Musical World

Musical World is a web application designed to allow users to upload their own songs, listen to songs already uploaded by others, and add songs to their favorite list. The project includes both an admin panel and a user portal.
Features

    User Registration and Authentication: Users must register and verify their accounts before uploading songs.
    Song Uploading: Users can upload their own songs, which will be stored in the database.
    Song Browsing and Favorites: Users can browse available songs and add them to their favorites list.
    Admin Panel: Admins can manage user accounts and uploaded content.

Database Setup

Before running the application, you'll need to set up the database:

    Create Database:
        Name the database musical_world.
        Import the tables.sql file located in the database folder to set up the necessary tables.

    Triggers and Stored Procedures:
        The application uses MySQL triggers and stored procedures. Make sure to create them in your MySQL environment (XAMPP, WAMP, etc.) before running the application.
    Trigger Code

    Trigger to track user contributions:


CREATE TRIGGER `IncrementCount` 
AFTER INSERT ON `upload_albums`
FOR EACH ROW 
UPDATE user 
SET user.contributions = user.contributions + 1 
WHERE NEW.singer_id = user.user_id;

Stored Procedure Code

Procedure to upload songs:



    DELIMITER $$
    CREATE DEFINER=`root`@`localhost` PROCEDURE `uploadsongs`(
        IN `singer_id` INT(11), 
        IN `song_name` VARCHAR(255), 
        IN `song_format` VARCHAR(255), 
        IN `singer_name` VARCHAR(255), 
        IN `song_image` VARCHAR(255), 
        IN `audio_file` VARCHAR(255)
    ) NO SQL
    INSERT INTO upload_albums(
        `singer_id`, 
        `song_name`, 
        `song_format`, 
        `singer_name`, 
        `song_image`, 
        `audio_file`
    ) VALUES(
        singer_id, 
        song_name, 
        song_format, 
        singer_name, 
        song_image, 
        audio_file
    );$$
    DELIMITER ;

Admin Panel Access

    Username: admin@gmail.com
    Password: 123