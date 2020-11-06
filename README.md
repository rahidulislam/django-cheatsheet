# django-cheatsheet


# Writing middlewares
link --> https://simpleisbetterthancomplex.com/tutorial/2016/07/18/how-to-create-a-custom-django-middleware.html

# 1. authentication from token in request headers

from django.utils.deprecation import MiddlewareMixin

from django.conf import settings

import requests

class MultipleProxyMiddleware(MiddlewareMixin):

    FORWARDED_FOR_FIELDS = [
        'HTTP_X_FORWARDED_FOR',
        'HTTP_X_FORWARDED_HOST',
        'HTTP_X_FORWARDED_SERVER',
    ]

    def process_request(self, request):
        """
        Rewrites the proxy headers so that only the most
        recent proxy is used.
        """
        # access_token = request.COOKIES.get("kalkeAccessToken")

        # if access_token:
        headers = {
            # "Authorization":request.headers.get('Authorization'),
            "Authorization":f"Bearer {access_token}",
            "Content-Type":"application/json"
        }
        r = requests.get(url='https://www.domain.com/im/api/v1/me',headers=headers)
        json = r.json()
        # print(r.json())
        request.META["user"] = json
        request.META["TEST"] = "HELLOW"
            # for field in self.FORWARDED_FOR_FIELDS:
            #     if field in request.META:
            #         if ',' in request.META[field]:
            #             parts = request.META[field].split(',')
            #             request.META[field] = parts[-1].strip()
        # else:
        request.META["user"] = None 
        
# 2. replacing the media url while processing request...

class StackOverflowMiddleware(MiddlewareMixin):

    def process_request(self, request):
        if request.is_secure():
            ssl_media_url = settings.MEDIA_URL.replace('http://','https://')
        else:
            print("No")
            ssl_media_url = settings.MEDIA_URL
        settings.MEDIA_URL = ssl_media_url
        
        return None
        


    def process_exception(self, request, exception):
        print("in res")
        if settings.DEBUG:
            print(exception.__class__.__name__)
            print(exception.message)
        return None
