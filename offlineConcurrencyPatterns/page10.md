[prev](page9.md)
# Паттерны offline конкурентного доступа

### Блокировка с низкой степенью детализации (Coarse-Grained Lock)

```java
class Version { 
    public static Version create() { //static create
        Version version = new Version(IdGenerator.INSTANCE.nextId(), 0,
                AppSessionManager.getSession().getUser(), now());
        version.isNew = true;//isNew = true;
        return version;
    }
    
    public void insert () {
        if (isNew()) { // if is new
            Connection conn = null;
            PreparedStatement pstmt = null;
            try {
                conn = ConnectionManager.INSTANCE.getConnection() ;
                pstmt = conn.prepareStatement(INSERT_SQL);
                pstmt.setLong(1, this.getId().lonqValue());
                pstmt.setLong(2, this. getvalue ()) ;
                pstmt.setString (3, this.getModifiedBy());
                pstmt.setTimestamp (4, this.getModified ());
                pstnt.executeUpdate ();
                AppSessionManager.getSession().getIdentityMap().putVersion(this) ;
                isNew = false; // isNew = false;
            } catch (SQLException sqlEx) {
                throw new SystemException("unexpected sal error inserting version", sqlEx);
            } finally {
                cleanupDBResources(conn, pstmt);
            }
        }
    }

    public void increment () throws ConcurrencyException {
        if (!isLocked()) { //if not locked
            Connection conn = null;
            PreparedStatement pstmt = null;
            try {
                conn = ConnectionManager.INSTANCE.getConnection();
                pstmt = conn.preparestatement(UPDATE_SQL);
                pstmt.setLong(1, value + 1); //increment value
                pstmt.setString(getModifiedBy());
                pstmt.setTimestamp(3, getModified());
                pstmt.setlong(4, id.longValue());
                pstmt.setLong(5, value);
                int rowCount = pstmt.executeUpdate();
                if (rowCount == 0) {//if row count is 0 throw exception
                    throwConcurrencyException();
                }
                valuet++;
                locked = true;
            } catch (SQLException sqlEx) {
                throw new SystemException("unexpected sql error incrementing version", sqlEx);
            } finally {
                cleanupDBResources(conn, pstmt);
            }
        }
    }
            
    private void throwConcurrencyException() {
        Version currentVersion = load(this.getId());
        throw new ConcurrencyException("version modified by " + currentVersion.modifiedBy +
                " at " + DateFormat.getDateTimeInstance().format (currentVersion. getModified ()));
    }
}
```
[next](page11.md)