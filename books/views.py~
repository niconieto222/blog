from django.shortcuts import render
from django.template import loader
from django.db.models import Q
from django.template import Context
from models import Book
from django.http import HttpResponse

def search(request):
	query = request.GET.get('q', '')
	if query:
		qset = (
			Q(title__icontains=query) |
			Q(authors__first_name__icontains=query) |
			Q(authors__last_name__icontains=query)
		)
		results = Book.objects.filter(qset).distinct()
	else:
		results = []
	t = loader.get_template("view1.html")
	c = Context({"results": results,"query": query})
	html = t.render(c)
	return HttpResponse(html)
