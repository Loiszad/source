---
title: SQLite
date: 2013-10-31 14:56:20
tags: SQLite 
categories: SQL
---
# 移动端轻量级数据库


```java

/**
 * Created by zhaojy on 2016/9/2.
 */
public class CrossDBManager {
  
  
    private Context mContext;
    public static CrossDBManager hpdbManager;
    private CrossDataBaseHelper dataBaseHelper;
    private SQLiteDatabase db;
  
    private CrossDBManager() {
        super();
    }
  
    private CrossDBManager(Context mContext) {
        this.mContext = mContext;
        dataBaseHelper = new CrossDataBaseHelper(mContext);
        db = dataBaseHelper.getWritableDatabase();
    }
  
    public static CrossDBManager getInstance(Context context) {
        if (hpdbManager == null) {
            synchronized (CrossDBManager.class) {
                hpdbManager = new CrossDBManager(context);
            }
        }
        return hpdbManager;
    }
  
    /**
     * 增
     *
     * @param key
     * @param value
     * @return
     */
    public boolean add(String key, String value) {
        try {
            if (db != null) {
                db.execSQL("insert into " + CrossConfiguration.DBTABLE_NAME +"(key,value) values(?,?)",new String[]{key,value});
                return true;
            } else {
                throw new Exception("Database init Failure");
            }
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }

  
    /**
     * 删
     *
     * @param key
     * @return
     */
    public boolean delete(String key) {
        try {
            if (db != null) {
                db.execSQL("delete from " + CrossConfiguration.DBTABLE_NAME + " where key=?",new String[]{key});
                return true;
            } else {
                throw new Exception("Database init Failure");
            }
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }

  
    /**
     * 改
     *
     * @param key
     * @return
     */
    public boolean update(String key, String newValue) {
        try {
            if (db != null) {
                db.execSQL("update " + CrossConfiguration.DBTABLE_NAME + " set value=? where key=?",new String[]{newValue,key});
                return true;
            } else {
                throw new Exception("Database init Failure");
            }
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }

  
    /**
     * 查
     *
     * @param key
     * @return 查询成功返回String 否则返回""
     */
    public String query(String key) {
        try {
            if (db != null) {
                Map<String, String> map = new HashMap<String, String>();
                Cursor cursor = db.rawQuery("select value from " + CrossConfiguration.DBTABLE_NAME + " where key=?", new
                        String[]{key});
                int cols_len = cursor.getColumnCount();
                while (cursor.moveToNext()) {
                    for (int i = 0; i < cols_len; i++) {
                        String cols_name = cursor.getColumnName(i);
                        String cols_value = cursor.getString(cursor
                                .getColumnIndex(cols_name));
                        if (cols_value == null) {
                            cols_value = "";
                        }
                        map.put(cols_name, cols_value);
                    }
                }
                cursor.close();
                return map.get("value");
            } else {
                throw new Exception("Database init Failure");
            }
        } catch (Exception e) {
            e.printStackTrace();
            return "";
        }
    }

  
    /**
     * close database
     */
//    public void closeDB() {
//        if (db != null) {
//            db.close();
//        }
//    }

}
```