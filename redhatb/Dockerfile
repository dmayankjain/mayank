FROM registry.access.redhat.com/ubi8/python-38

# Install basic dependencies
USER root
RUN yum install mssql-tools unixODBC-devel

# Add SQL Server ODBC Driver 17 for Centos
RUN curl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/mssql-release.repo
RUN ACCEPT_EULA=Y yum install -y msodbcsql17

# Deploying the code
RUN mkdir /code
WORKDIR /code
COPY requirements.txt /code/
RUN pip install -r requirements.txt
COPY . /code/
RUN useradd -ms /bin/bash appuser
RUN chown -R appuser:appuser /code/
USER appuser
EXPOSE 8000
ENTRYPOINT ["python", "manage.py"] 
CMD ["runserver", "0.0.0.0:8000"]

