```
from sqlalchemy import Column, String, create_engine, Integer, JSON, DATETIME
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker, scoped_session

from setting.settings import mysqldb_driver, sql_orm_config

# 创建对象的基类:
Base = declarative_base()


class BaseSetting(Base):
    __abstract__ = True
    __table_args__ = {  # 可以省掉子类的 __table_args__ 了
        'mysql_engine': 'InnoDB',
        'mysql_charset': 'utf8mb4'
    }


# 定义User对象:
class ZsxqModel(BaseSetting):
    # 表的名字:
    __tablename__ = 'zsxq'

    # 表的结构:
    id = Column(Integer, primary_key=True)
    content = Column(JSON)
    label = Column(String)
    created = Column(DATETIME)
    updated = Column(DATETIME)
    owner_name = Column(String)


engine = create_engine(
    mysqldb_driver,
    encoding=sql_orm_config["encoding"],
    echo=sql_orm_config["echo"],
    pool_size=sql_orm_config["pool_size"],
    max_overflow=sql_orm_config["max_overflow"],
    pool_timeout=sql_orm_config["pool_timeout"])

# 创建DBSession类型:
db = scoped_session(sessionmaker(autocommit=sql_orm_config["autocommit"], autoflush=sql_orm_config["autoflush"], bind=engine))
```