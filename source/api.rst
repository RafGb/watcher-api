.. _api:


API v2
******


Conventions
===========


Security Parameters
-------------------

headers
   * **X-Vsaas-Apikey** (*string*) : Watcher API Key

   * **X-Vsaas-Session** (*string*) : Session key, for logged in users


Collections
-----------

query
   * **search** (*string*): Substring to filter collection items
     (generally by name, title and comment)

   * **limit** (*integer*): Number of items returned (for collections)

   * **offset** (*integer*): Number of skipped items (for collections)

headers
   * **X-Page-Limit** (*integer*)

   * **X-Page-Offset** (*integer*)


HTTP codes
----------

* **200** Success

* **400** ValidationError

* **400** BadRequest

* **403** Forbidden

* **403** ApikeyExpired

* **403** WrongApikey

* **404** NotFound

* **500** ApplicationError


Security Roles
--------------

* guest

* authenticated user

* administrator

+----------------------+---------------------------------------------------------------+-------------------------------------+
| Resource             | Operation                                                     | Description                         |
+======================+===============================================================+=====================================+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+
+----------------------+---------------------------------------------------------------+-------------------------------------+


Authentication
==============

``POST /vsaas/api/v2/auth/generate-autologin-token``

   Generates an autologin token Used as an integration point with a
   custom service

   :Request JSON Object:
      * **login** (*string*) --

      * **lifetime** (*integer*) --

      * **valid_till** (*integer*) --

   :Response JSON Object:
      * **autologin_token** (*string*) --

``POST /vsaas/api/v2/auth/forgot-password``

   Sends an email contains password reset URL

   :Request JSON Object:
      * **login** (*string*) -- User's login (optional)

      * **email** (*string*) -- User's notification email (optional)

   :Status Codes:
      * 200 OK -- Email sent

      * 403 Forbidden -- Login or email not found

``POST /vsaas/api/v2/auth/check-login``

   Checks user login and password

   :Request JSON Object:
      * **login** (*string*) -- User login

      * **password** (*string*) -- User password

   :Status Codes:
      * 200 OK -- login and password are correct

      * 403 Forbidden -- user does not exist or password is incorrect

``GET /vsaas/api/v2/auth/whoami``

   Returns session information

   :Request Headers:
      * *X-Vsaas-Session string* -- session key, optional

   :Response JSON Object:
      * **login** (*string*) -- current login

      * **is_admin** (*boolean*) -- current user can manage cameras,
        users, and groups

``POST /vsaas/api/v2/auth/login``

   Logs user in

   :Request JSON Object:
      * **login** (*string*) -- User login

      * **password** (*string*) -- User password

   :Response JSON Object:
      * **session** (*string*) -- SessionId

      * **login** (*bool*) --

      * **is_admin** (*bool*) --

      * **notification_email** (*bool*) --


Camera Management
=================

``POST /vsaas/api/v2/cameras/import``

``POST /vsaas/api/v2/cameras``

   Returns camera list

   :Request JSON Object Array:
      * **name** (*string*): Stream identifier
      * **access** (*string*)
      * **agent_id** (*string*)
      * **agent_key** (*string*)
      * **agent_model** (*string*)
      * **agent_pin** (*string*)
      * **agent_serial** (*string*)
      * **agent_status** (*object*)
        * **connected_at** (*string*)
        * **id** (*string*)
        * **ip** (*string*)
        * **local_ip** (*string*)
        * **streampoint** (*string*)
        * **version** (*string*)
      * **comment** (*string*)
      * **coordinates** (*string*)
      * **dvr_depth** (*integer*)
      * **dvr_enabled** (*boolean*)
      * **dvr_path** (*string*)
      * **enabled** (*boolean*)
      * **groups** (*object array*)
        * **id** (*string*)
        * **title** (*string*)
      * **motion_detector** (*boolean*)
      * **onvif_profile** (*string*)
      * **onvif_ptz** (*boolean*)
      * **onvif_url** (*string*)
      * **owner** (*string*)
      * **permissions** (*string*)
      * **playback_config** (*object*)
        * **token** (*string*)
      * **postal_address** (*string*)
      * **preview_url** (*string*)
      * **server** (*string*)
      * **static** (*boolean*)
      * **stream_status** (*object*)
        * **alive** (*boolean*)
        * **bitrate** (*integer*)
        * **lifetime** (*integer*)
        * **server** (*string*)
        * **source_error** (*string*)
      * **stream_url** (*string*)
      * **substream_url** (*string*)
      * **thumbnails** (*boolean*)
      * **thumbnails_url** (*string*)
      * **title** (*string*): Human readable title
      * **user_attributes** (*object*)
        * **comment** (*string*)
        * **favorite** (*string*)
        * **title** (*string*)
``GET /vsaas/api/v2/cameras``

   Returns camera list

   :Request JSON Object Array:
      * **name** (*string*): Stream identifier
      * **access** (*string*)
      * **agent_id** (*string*)
      * **agent_key** (*string*)
      * **agent_model** (*string*)
      * **agent_pin** (*string*)
      * **agent_serial** (*string*)
      * **agent_status** (*object*)
        * **connected_at** (*string*)
        * **id** (*string*)
        * **ip** (*string*)
        * **local_ip** (*string*)
        * **streampoint** (*string*)
        * **version** (*string*)
      * **comment** (*string*)
      * **coordinates** (*string*)
      * **dvr_depth** (*integer*)
      * **dvr_enabled** (*boolean*)
      * **dvr_path** (*string*)
      * **enabled** (*boolean*)
      * **groups** (*object array*)
        * **id** (*string*)
        * **title** (*string*)
      * **motion_detector** (*boolean*)
      * **onvif_profile** (*string*)
      * **onvif_ptz** (*boolean*)
      * **onvif_url** (*string*)
      * **owner** (*string*)
      * **permissions** (*string*)
      * **playback_config** (*object*)
        * **token** (*string*)
      * **postal_address** (*string*)
      * **preview_url** (*string*)
      * **server** (*string*)
      * **static** (*boolean*)
      * **stream_status** (*object*)
        * **alive** (*boolean*)
        * **bitrate** (*integer*)
        * **lifetime** (*integer*)
        * **server** (*string*)
        * **source_error** (*string*)
      * **stream_url** (*string*)
      * **substream_url** (*string*)
      * **thumbnails** (*boolean*)
      * **thumbnails_url** (*string*)
      * **title** (*string*): Human readable title
      * **user_attributes** (*object*)
        * **comment** (*string*)
        * **favorite** (*string*)
        * **title** (*string*)
``POST /vsaas/api/v2/cameras/(path: name)/ptz/stop``

   Stops camera's movement

``POST /vsaas/api/v2/cameras/(path: name)/ptz/move``

   Starts camera's movement

``POST /vsaas/api/v2/cameras/(path: name)/user_attributes``

``GET /vsaas/api/v2/cameras/(path: name)/agent``

   Returns agent status

   :Status Codes:
      * 200 OK -- Agent information

      * 404 Not Found -- No Agent

``PUT /vsaas/api/v2/cameras/(path: name)``

``GET /vsaas/api/v2/cameras/(path: name)``


User Management
===============

``POST /vsaas/api/v2/users``

   Adds user or users

   :Request Headers:
      * Content-Type -- ``application/json`` or ``text/csv``

   :Request JSON Object:
      * **login** (*string*)
      * **authorized_ip** (*string*)
      * **camera_count** (*string*)
      * **dvr_allowed** (*boolean*)
      * **enabled** (*boolean*)
      * **external_id** (*string*)
      * **groups** (*object array*)
        * **group_id** (*integer*)
        * **can_dvr** (*boolean*)
        * **can_manage_cameras** (*boolean*)
        * **can_manage_users** (*boolean*)
        * **can_ptz** (*boolean*)
        * **comment** (*string*)
        * **group** (*object*)
          * **title** (*string*)
          * **id** (*integer*)
          * **note** (*string*)
        * **order_num** (*integer*)
        * **usergroup_id** (*integer*)
      * **id** (*integer*)
      * **is_admin** (*boolean*)
      * **note** (*string*)
      * **notification_email** (*string*)
      * **password** (*string*)
``GET /vsaas/api/v2/users``

   Returns a user list

   :Response JSON Object Array:
      * **login** (*string*)
      * **authorized_ip** (*string*)
      * **camera_count** (*string*)
      * **dvr_allowed** (*boolean*)
      * **enabled** (*boolean*)
      * **external_id** (*string*)
      * **groups** (*object array*)
        * **group_id** (*integer*)
        * **can_dvr** (*boolean*)
        * **can_manage_cameras** (*boolean*)
        * **can_manage_users** (*boolean*)
        * **can_ptz** (*boolean*)
        * **comment** (*string*)
        * **group** (*object*)
          * **title** (*string*)
          * **id** (*integer*)
          * **note** (*string*)
        * **order_num** (*integer*)
        * **usergroup_id** (*integer*)
      * **id** (*integer*)
      * **is_admin** (*boolean*)
      * **note** (*string*)
      * **notification_email** (*string*)
      * **password** (*string*)
``PUT /vsaas/api/v2/users/(int: id)``

   Modifies user

   :Query Parameters:
      * **id** (*integer*) -- User identifier

   :Request JSON Object Array:
      * **login** (*string*)
      * **authorized_ip** (*string*)
      * **dvr_allowed** (*boolean*)
      * **enabled** (*boolean*)
      * **external_id** (*string*)
      * **id** (*integer*)
      * **is_admin** (*boolean*)
      * **note** (*string*)
      * **notification_email** (*string*)
      * **password** (*string*)
   :Response JSON Object Array:
      * **login** (*string*)
      * **authorized_ip** (*string*)
      * **dvr_allowed** (*boolean*)
      * **enabled** (*boolean*)
      * **external_id** (*string*)
      * **id** (*integer*)
      * **is_admin** (*boolean*)
      * **note** (*string*)
      * **notification_email** (*string*)
      * **password** (*string*)
``DELETE /vsaas/api/v2/users/(int: id)``

   Removes user

   :Query Parameters:
      * **id** (*integer*) -- User identifier

``GET /vsaas/api/v2/users/(int: id)``

   Returns a single user

   :Query Parameters:
      * **id** (*integer*) -- User identifier

   :Response JSON Object:
      * **login** (*string*)
      * **authorized_ip** (*string*)
      * **camera_count** (*string*)
      * **dvr_allowed** (*boolean*)
      * **enabled** (*boolean*)
      * **external_id** (*string*)
      * **groups** (*object array*)
        * **group_id** (*integer*)
        * **can_dvr** (*boolean*)
        * **can_manage_cameras** (*boolean*)
        * **can_manage_users** (*boolean*)
        * **can_ptz** (*boolean*)
        * **comment** (*string*)
        * **group** (*object*)
          * **title** (*string*)
          * **id** (*integer*)
          * **note** (*string*)
        * **order_num** (*integer*)
        * **usergroup_id** (*integer*)
      * **id** (*integer*)
      * **is_admin** (*boolean*)
      * **note** (*string*)
      * **notification_email** (*string*)
      * **password** (*string*)

Group Management
================

``POST /vsaas/api/v2/groups``

   Creates group or groups

   :Request JSON Object Array:
      * **title** (*string*)
      * **id** (*integer*)
      * **note** (*string*)
   :Response JSON Object Array:
      * **title** (*string*)
      * **id** (*integer*)
      * **note** (*string*)
``GET /vsaas/api/v2/groups``

   Returns a group

   :Response JSON Object Array:
      * **title** (*string*)
      * **camera_count** (*integer*)
      * **id** (*integer*)
      * **note** (*string*)
      * **user_count** (*integer*)
``POST /vsaas/api/v2/groups/(int: group_id)/cameras/(path:
name)/order``

   Modifies camera's position inside a group

   :Query Parameters:
      * **group_id** (*integer*) -- Group identifier

      * **name** (*integer*) -- Camera name

``PUT /vsaas/api/v2/groups/(int: group_id)/cameras/(path: name)``

   Modifies camera's parameters inside a group

   :Query Parameters:
      * **group_id** (*integer*) -- Group identifier

      * **name** (*integer*) -- Camera name

``DELETE /vsaas/api/v2/groups/(int: group_id)/cameras/(path: name)``

   Removes camera from group

   :Query Parameters:
      * **group_id** (*integer*) -- Group identifier

      * **name** (*integer*) -- Camera name

``POST /vsaas/api/v2/groups/(int: group_id)/cameras``

   Adds camera to group

   :Query Parameters:
      * **group_id** (*string*) -- Group identifier

   :Request JSON Object:
      * **camera_id** (*string*) -- Camera name

   :Response JSON Object:
      * **camera_id** (*string*)
      * **group_id** (*integer*)
      * **camera** (*object*)
        * **name** (*string*): Stream identifier
        * **access** (*string*)
        * **agent_id** (*string*)
        * **agent_key** (*string*)
        * **agent_model** (*string*)
        * **agent_pin** (*string*)
        * **agent_serial** (*string*)
        * **comment** (*string*)
        * **coordinates** (*string*)
        * **dvr_depth** (*integer*)
        * **dvr_enabled** (*boolean*)
        * **dvr_path** (*string*)
        * **enabled** (*boolean*)
        * **motion_detector** (*boolean*)
        * **onvif_profile** (*string*)
        * **onvif_ptz** (*boolean*)
        * **onvif_url** (*string*)
        * **owner** (*string*)
        * **postal_address** (*string*)
        * **preview_url** (*string*)
        * **server** (*string*)
        * **static** (*boolean*)
        * **stream_url** (*string*)
        * **substream_url** (*string*)
        * **thumbnails** (*boolean*)
        * **thumbnails_url** (*string*)
        * **title** (*string*): Human readable title
      * **comment** (*string*)
      * **id** (*integer*)
      * **order_num** (*integer*)
``GET /vsaas/api/v2/groups/(int: group_id)/cameras``

   Returns cameras belonging to the group

   :Response JSON Object:
      * **camera_id** (*string*)
      * **group_id** (*integer*)
      * **camera** (*object*)
        * **name** (*string*): Stream identifier
        * **access** (*string*)
        * **agent_id** (*string*)
        * **agent_key** (*string*)
        * **agent_model** (*string*)
        * **agent_pin** (*string*)
        * **agent_serial** (*string*)
        * **comment** (*string*)
        * **coordinates** (*string*)
        * **dvr_depth** (*integer*)
        * **dvr_enabled** (*boolean*)
        * **dvr_path** (*string*)
        * **enabled** (*boolean*)
        * **motion_detector** (*boolean*)
        * **onvif_profile** (*string*)
        * **onvif_ptz** (*boolean*)
        * **onvif_url** (*string*)
        * **owner** (*string*)
        * **postal_address** (*string*)
        * **preview_url** (*string*)
        * **server** (*string*)
        * **static** (*boolean*)
        * **stream_url** (*string*)
        * **substream_url** (*string*)
        * **thumbnails** (*boolean*)
        * **thumbnails_url** (*string*)
        * **title** (*string*): Human readable title
      * **comment** (*string*)
      * **id** (*integer*)
      * **order_num** (*integer*)
``PUT /vsaas/api/v2/groups/(int: group_id)/users/(int: user_id)``

   Modifies user's permissions inside a group

   :Query Parameters:
      * **group_id** (*integer*) -- Group identifier

      * **user_id** (*integer*) -- User identifier

   :Request JSON Object:
      * **group_id** (*integer*)
      * **user_id** (*integer*)
      * **can_dvr** (*boolean*)
      * **can_manage_cameras** (*boolean*)
      * **can_manage_users** (*boolean*)
      * **can_ptz** (*boolean*)
      * **comment** (*string*)
      * **id** (*integer*)
      * **order_num** (*integer*)
   :Response JSON Object:
      * **group_id** (*integer*)
      * **user_id** (*integer*)
      * **can_dvr** (*boolean*)
      * **can_manage_cameras** (*boolean*)
      * **can_manage_users** (*boolean*)
      * **can_ptz** (*boolean*)
      * **comment** (*string*)
      * **group** (*object*)
        * **title** (*string*)
        * **id** (*integer*)
      * **id** (*integer*)
      * **order_num** (*integer*)
      * **user** (*object*)
        * **login** (*string*)
        * **dvr_allowed** (*boolean*)
        * **enabled** (*boolean*)
        * **id** (*integer*)
        * **is_admin** (*boolean*)
      * **usergroup_id** (*integer*)
``DELETE /vsaas/api/v2/groups/(int: group_id)/users/(int: user_id)``

   Removes user from group

   :Query Parameters:
      * **group_id** (*integer*) -- Group identifier

      * **user_id** (*integer*) -- User identifier

``POST /vsaas/api/v2/groups/(int: group_id)/users``

   Adds user to group

   :Query Parameters:
      * **id** (*string*) -- Group identifier

   :Request JSON Object:
      * **group_id** (*integer*)
      * **user_id** (*integer*)
      * **can_dvr** (*boolean*)
      * **can_manage_cameras** (*boolean*)
      * **can_manage_users** (*boolean*)
      * **can_ptz** (*boolean*)
      * **comment** (*string*)
      * **id** (*integer*)
      * **order_num** (*integer*)
   :Response JSON Object:
      * **group_id** (*integer*)
      * **user_id** (*integer*)
      * **can_dvr** (*boolean*)
      * **can_manage_cameras** (*boolean*)
      * **can_manage_users** (*boolean*)
      * **can_ptz** (*boolean*)
      * **comment** (*string*)
      * **group** (*object*)
        * **title** (*string*)
        * **id** (*integer*)
      * **id** (*integer*)
      * **order_num** (*integer*)
      * **user** (*object*)
        * **login** (*string*)
        * **dvr_allowed** (*boolean*)
        * **enabled** (*boolean*)
        * **id** (*integer*)
        * **is_admin** (*boolean*)
      * **usergroup_id** (*integer*)
``PUT /vsaas/api/v2/groups/(int: id)``

   Modifies a group

   :Query Parameters:
      * **id** (*string*) -- Group fdentifier

   :Response JSON Object Array:
      * **title** (*string*)
      * **id** (*integer*)
      * **note** (*string*)
``DELETE /vsaas/api/v2/groups/(int: id)``

   Deletes a group

   :Query Parameters:
      * **id** (*string*) -- Group identifier

``GET /vsaas/api/v2/groups/(int: id)``

   Returns a group list

   :Response JSON Object Array:
      * **title** (*string*)
      * **camera_count** (*integer*)
      * **id** (*integer*)
      * **note** (*string*)
      * **users** (*object array*)
        * **group_id** (*integer*)
        * **user_id** (*integer*)
        * **can_dvr** (*boolean*)
        * **can_manage_cameras** (*boolean*)
        * **can_manage_users** (*boolean*)
        * **can_ptz** (*boolean*)
        * **comment** (*string*)
        * **order_num** (*integer*)
        * **user** (*object*)
          * **login** (*string*)
          * **dvr_allowed** (*boolean*)
          * **enabled** (*boolean*)
          * **id** (*integer*)
          * **is_admin** (*boolean*)
        * **usergroup_id** (*integer*)